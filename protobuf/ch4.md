Specifying import paths
---

In order to import files that are in a given location, we can use the --proto_path flag or its short version -I (capital I). So, we could have the following .proto file (a.proto):

```
syntax = "proto3";
import "b.proto"; // this is the path
message A {
  B b = 1;
}
```

Without going into too much detail about why this is the case, protoc tells us that it basically cannot figure out if two paths are equivalent. In our case, the two paths, proto/b and the current path (.), are not equivalent, but it does not matter. protoc needs to know where all the files are. We can solve that by including the current path. We can run the following command:
```
$ protoc --cpp_out=. --proto_path=. --proto_path=proto/b a.proto
```

Encoding data to type with --encode
---

We can now encode the .txtpb file data into a User message by executing the following command on Linux and macOS:

```
$ cat user.txtpb | protoc --encode=User user.proto
```
And we use this command on Windows:
```
$ Get-Content user.txtpb | protoc --encode=User user.proto
```

Next, notice that we are using the message as a value for the --encode flag. 
This is because we need to let protoc know which type it needs to use to encode the data.
Note that if you have this type inside a package, you will need to specify the full name to the --encode flag; 
otherwise, it will not compile. For example, for using Well-Known Types that are under the google.protobuf package,
you will need to write the following:
```
$ protoc --encode=google.proto.${TYPE_NAME} ${PATH_TO_WELL_KNOWN_TYPE}
```

Decoding data to type with --decode
---

we can now see how to use --decode. It is very similar to --encode. It takes data on the standard input, decodes it into a type, and it needs to know where to find the type definition. It looks like this:
```
$ cat user.bin | protoc --decode=User user.proto
```
