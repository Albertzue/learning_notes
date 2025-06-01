Less boilerplate
---
it is easier to write the txtpb file for the following reasons:

1. There are no outer braces for the first level
2. There are no commas between the fields
3. The keys are not enclosed by double quotes
4. You can omit colons when defining a field that uses a user-defined type (see amount)
 
Type safety
---
As we know, Protobuf is designed to be type-safe. This means that if we passed the wrong value to a txtpb file and tried to serialize/deserialize it, Protobuf would give us messages like the following (set "9" string to integer field):
```
Providing "9" instead of 9 to units field: Expected integer, got: "9"
```

Headers and comments
---
```
# proto-file: some/proto/my_file.proto
# proto-message: MyMessage
```
This shows us that the following data are supposed to be serialized using the message definition called MyMessage, 
and that the definition of that message is in the file some/proto/my_file.proto.

we can save some time by adding a comment right next to the field. This could look like the following:
```
amount {
  currency_code: "USD"
  units: 9 # 9 dollars
  nanos: 990000000 # 99 cents
}
```

Oneofs
---
```
syntax = "proto3";
import "google/protobuf/duration.proto";
message AudioBook {
  google.protobuf.Duration duration = 1;
  //...
}
message HardCover {
  uint64 pages = 1;
  //...
}
message Book {
  oneof Type {
    AudioBook audio_book = 1;
    HardCover hard_cover = 2;
  }
}
```
Passing the following data is valid:
```
hard_cover {
  pages: 200
}
```
This is because we are only setting one field of the oneof inside book. Now, if we set both audio_book and hard_cover, like this:
```
hard_cover {
  pages: 200
}
audio_book {
  duration {
    seconds: 9000 # 2h30
  }
}
```
we would get the following error:
```
Field "audio_book" is specified along with field "hard_cover", another me
```
