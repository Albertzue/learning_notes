Syntax
---

EBNF – Syntax statement
```
version = "proto2" | "proto3" | "editions"
syntax = "syntax" "=" ("'" version "'" | '"' version '"') ";"
As you can see, there are three versions that we can pass to the syntax statement:
```
1. proto2
2. proto3
3. editions
Now, all of this is a little bit obscure, and these names, especially proto2 and proto3, are misnomers.
proto3 is not really a better version than proto2; they just provide different features. For example,
the internals of Protobuf are written in proto2, and most of the code written outside of Protobuf is written in proto3.

Edition
---

As we mentioned previously in the syntax subsection, editions will provide more flexibility to the language.
We will be able to roll out ameliorations step by step by simply incrementing our version in the edition statement
```
version = "2023" | "2024" | ...
edition = "edition" "=" ("'" version "'" | '"' version '"') ";"
```
Now, it is important to note that the version mentioned in the EBNF syntax is different than the previous version we defined. 
The Protobuf team chose to make editions named after the year they were released (e.g., 2023, 2024, etc.).

Package
---
Protobuf lets us define units of related schemas with packages. This can be useful for separating concerns and adding an extra layer of type safety
As you can see in the syntax, packages accept a fully qualified identifier. This means that the following are the correct names:
```
google
google.protobuf
google.protobuf.v2
```
With these names, we can reference the definitions in them by prepending the name of the package to the type. 
If we have a message called Person living under the package packt.protobuf.ch2, we could reference it by writing packt.protobuf.ch2.Person 
from outside the package, or Person if we were referencing it from within the packt.protobuf.ch2 package.

Import
---
The most common example of reusability is using the well-known types already provided in Protobuf (more on that in the “Out-of-the-box types” section). For example, we can use the Duration type by importing the duration.proto file:
```
import "google/protobuf/duration.proto";
```

the recommendation is to keep all the relevant definitions together and split the definitions that can be reused separately. 
duration.proto is such an example of splitting the definitions to increase reusability.
In this case, we want to only import Duration and reuse it in multiple places

Finally, you can notice the two keywords: weak and public. 
I added weak for the sake of completeness, but this is only used internally at Google.
So, let us forget about this one. However, public is interesting since it lets you create transitive dependencies. 
This means that if a.proto imports b.proto publicly, any proto file importing a.proto will also have access to the definitions in b.proto.

Option
---

An example of this is the option called deprecated, which, depending on the programming language you are using,
will mark all the types in the file as deprecated. Here is what it looks like:
```
option deprecated = true;
```

User-defined types
---------------

enum
---
```
enum PhoneType {
  PHONE_TYPE_MOBILE = 0;
  PHONE_TYPE_HOME = 1;
  //...
}
```

Now, the main difference between enums in proto2 and proto3 is that enums in proto3 are open. 
An open enum is an enum that does not reject values that are not defined. Let us take the example of setting a field with the type PhoneType to a value of 3. 
In proto2, it would simply be impossible to do so because the compiler would refuse such a value. 
However, the proto3 compiler would accept the value.

For options in the enum body, this is very similar to options at the file level. It looks like this:
```
enum OldPhoneType {
  option deprecated = true;
  //...
}
```

For the value options, they are a little bit different. We write them between square braces ([ ]) and separate them with commas. It looks like this:
```
enum PhoneType {
  //...
  // disclosure: description is a custom option!
  PHONE_TYPE_FAX = 3 [deprecated = true, description = "who uses fax 
  machines anymore?"];
}
```

Message
---

Field
---
A message is mainly a collection of fields. They represent the actual data to be serialized and deserialized:
```
bool is_authenticated = 1;
```

Now, in the case of fields, the main difference that you have between proto2 and proto3 is the fact that in proto2, 
you can have the labels required and optional in front of the field. In proto3, every field is optional by default. 
This means that we can set a value (or not) in a field, whereas in proto2, having a required field without a value would not compile.

Next, there is the third label called repeated. This is a label that we can use in both versions. 
It means that the field is a list of the following type (this defaults to an empty list if not set). For example, 
if we wanted to have a person with multiple middle names, we could use the following:
```
repeated string middle_names = 1;
```

Tags are numerical identifiers for fields. When we write something like the following:
```
int32 age = 1;
```
it does not mean we are setting the value 1 to age;
it means we set the identifier for this field to 1.
This is how Protobuf knows where to deserialize data. Protobuf will serialize data to binary in the following format:
```
(id + type) value
```

Reserved
---
Reserving a field tag and/or a field name makes the reserved element not usable anymore
```
message InvalidField {
  reserved 1;
  uint32 id = 1;
}
```
will not compile because we reserved the tag 1. Similarly,
```
message InvalidField {
  reserved "id";
  uint32 id = 1;
}
```
will not compile because we reserved the name id.

nother thing to mention is that we can define more complex ranges of tags. If we wanted to remove the tags from 1 to 10, we would write the following:
```
reserved 1 to 10;
```
The start and the end of the range are inclusive. Meaning that we reserved the tag from 1 to 10 and not from 1 to 9.
```
reserved 1 to max;
```
In this case, we reserved all the possible tags. This is obviously not useful because it would mean we cannot define any field in the message.

MapField
---
In Protobuf, we can write a map like this:
```
map<string, int32> occurrences = 1;
```
Notice that not all the types we saw previously in the field subsection are available as key types. We cannot use float/double, bytes, or message types as key types. Other than that restriction, as you can see, maps are similar to fields.

Oneof
---

Sometimes, we need to explicitly set one value or the other. This kind of mutually exclusive data can be defined with oneof fields. They wrap multiple fields and enforce the logic of only one of those fields having a value.
```
oneof result {
  Success success = 1;
  Error error = 2;
}
```

Message
---
we can have a maximum of 31 nested messages.

Services
---

service is designed for Protobuf interaction with RPC frameworks, such as gRPC. 
```
service BookService {
  rpc ListBooks(ListBooksRequest) returns (ListBooksResponse);
  rpc GetBook(GetBookRequest) returns (Book);
  rpc CreateBook(CreateBookRequest) returns (Book);
  rpc UpdateBook(UpdateBookRequest) returns (Book);
  rpc DeleteBook(DeleteBookRequest) returns (google.protobuf.Empty);
}
```

It defines a contract for the BookService. The server will implement the List, Get, Create, Update, and Delete operations. Each of them will take some data as input (the types ending with Request) and will return some data as output (ListBooksResponse, Book, and google.protobuf.Empty). The client will also be aware of these parameters and outputs so that they can create requests and get responses back from the server.


Out-of-the-box types
---
On top of all the scalar types that Protobuf provides as part of the language, it also provides some already-defined types called **well-known types (WKTs)**. All these types can be found in the src/google/protobuf folder in the GitHub repository (https://github.com/protocolbuffers/protobuf/tree/main/src/google/protobuf), and they are all defined under the **google.protobuf** package.

Here is a list of the most common WKTs available:
```
Duration
Timestamp
FieldMask
Any
Struct
```

here is how you can use these types:

```
import "google/protobuf/duration.proto";
import "google/protobuf/timestamp.proto";
message RunRace {
  google.protobuf.Duration length = 1;
}
message Account {
  google.protobuf.Timestamp updated_at = 1;
}
```

FieldMask
---

Sometimes, we need a way to select a subset of fields for a given message. Generally, this is done to reduce the payload size and make
```
message FieldMask {
  repeated string paths = 1;
}
```
```
message Book {
  oneof book_type {
    PaperBack paperback = 1;
    Ebook ebook = 2;
    AudioBook audiobook = 3;
  }
}
```
If we only care about the paperback information, we would have the paperback path directly, not book_type.paperback.

Any
---
As its name suggests, Any can represent any Protobuf message. We can serialize a message and keep the raw bytes inside it. This is basically a dynamic object.

The Any definition looks like this (simplified):
```
message Any {
  string type_url = 1;
  bytes value = 2;
}
```

Struct
---
The last common WKT is Struct. This one also represents a dynamic object but in a way that is similar to what the JSON format is doing. The definition of Struct looks like the following (simplified):
```
message Struct {
  map<string, Value> fields = 1;
}
message Value {
  oneof kind {
    NullValue null_value = 1;
    double number_value = 2;
    string string_value = 3;
    bool bool_value = 4;
    Struct struct_value = 5;
    ListValue list_value = 6;
  }
}
enum NullValue {
  NULL_VALUE = 0;
}
message ListValue {
  repeated Value values = 1;
}
```
As you can see, this example uses a little bit of everything that we have learned so far: messages, oneofs, fields, enums, repeated fields, and maps.
