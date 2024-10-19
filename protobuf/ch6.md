Disabling tags – reserved tags
---

Protobuf has a concept called reserved tags. This means that these tags are made unusable by developers when they are updating a message. This looks like this:
```
message Id {
  reserved 1;
}
```

instead of directly changing the field type (in v2.proto), we are going to change the field tag to 2. Now, v2.proto looks like this:
```
syntax = "proto3";
message Id {
  uint64 value = 2;
}
```


We’ve effectively solved the problem. However, another is arising from what we did. Since we changed the tag from 1 to 2, we released tag 1 for reuse. Any new developer could come in and add a field with a tag of 1. However, this would lead to the problems we talked about previously (overflow, wrong type, and so on).

To avoid this, we must add a reserved tag, like so (proto/v2/id.proto):
```
syntax = "proto3";
message Id {
  reserved 1;
  uint64 value = 2;
}
```
Disabling field names – reserved names
---

First, we need to add the go_package option to our proto file (proto/v1/id.proto) to tell the protoc compiler in which Go package we would like to generate the code. In my case, the Go module is github.com/PacktPublishing/Protocol-Buffers-Handbook/chapter6 and I have a subdirectory called proto, so I will have the following:

```
syntax = "proto3";
option go_package = "github.com/PacktPublishing/Protocol-Buffers-Handbook/chapter6/proto";
message Id {
  uint32 value = 1;
}
```
```
$ protoc --go_out=. --go_opt=module=github.com/PacktPublishing/Protocol-Buffers-Handbook/chapter6 proto/v1/id.proto
```
This command will take the go_package value in id.proto, remove the prefix value that’s passed into the go_opt module

```
syntax = "proto3";
option go_package = "github.com/PacktPublishing/Protocol-Buffers-Handbook/chapter6/proto";
message Id {
  reserved 1;
  reserved "value";
  string uuid = 2;
}
```
With this, our code will never see a value field for future versions.

As you can see, this is more like protection for the code. This is because, as you may recall, names are not encoded in the binary, only tags and types are. We saw encoding/decoding safety with reserved tags and now, we have code safety with reserved names.

Here’s the list of rules that we should follow if we need to maintain backward and forward compatibility:

- **Never remove a reserved statement.** This probably goes without saying but reserved statements are here to protect us. Do not remove or modify them; otherwise, you will get undefined behaviors.
- **Never modify a field tag.** This will lead Protobuf to decode data into unknown fields between versions. This means you will not receive that data and get a default value.
- **Avoid reusing a field tag.** As we saw, this can cause problems such as integer overflow or other problems due to type conversion. It is better to just add a new field to deal with the new data. Remember that tags are encoded as varints.
- **Always add a reserved tag when deleting a field.** This prevents newer versions from accidentally reusing that tag and thus leads to the problems mentioned in the previous point.
- **Consider adding a reserved name.** This is optional but this might have a good long-term impact on the code you are writing. As we saw, this can prevent the reuse of field names and protect against implicit conversions.
- **Consider making packages named after versions.** We did not talk about this during this chapter, but we could package each version with a version name (for example, package v3). This would lead developers to be more explicit about which version of the message they are using.
