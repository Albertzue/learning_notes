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
