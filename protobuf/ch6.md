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
