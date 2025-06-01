Variable-length integers (varints)
---

We can write the following proto file (varint/encoding.proto):
```
syntax = "proto3";
message Encoding {
  int32 i32 = 1;
}
```
Then, we can define the data in a txtpb file, like so:
```
i32: 128
```
Now that we have that, we can run protoc with the --encode flag and see the result. On Linux/Mac, we can run the following command:
```
$ cat int32.txtpb | protoc --encode=Encoding encoding.proto | hexdump –C
```

#### Important message
Unfortunately, PowerShell does not deal well with external commands like protoc.
As such, I will not provide Windows commands by fear of misleading PowerShell users.
At the time of writing this, the best way to follow the following sections on Windows is to use Windows Subsystem for Linux (WSL).

To summarize, we have the following for encoding:
```
         10000000 // Original input (big-endian).
 0000001  0000000 // Split into 7-bits groups
 0000000  0000001 // Convert to little-endian
10000000 00000001 // Add MSBs
```
**most significant bit (MSB)** 

We have the following for decoding:
```
10000000 00000001 // Original input (little-endian)
 0000000  0000001 // Drop MSBs.
 0000001  0000000 // Convert to big-endian
   00000010000000 // Concatenate
              128 // Result
```

How to choose between integer types
---
#### Number range
when choosing an integer type, we need to be aware of the range of values needed for a specific use case.

#### Sign
In Protobuf, another way of selecting the range of values we can handle is by selecting the sign of an integer type. 
For those of you who are familiar with most statically typed languages, 
you are already familiar with this. We can choose between an unsigned int (uint) and an int.

#### Data distribution

Before the improvement, the comparison with the JSON payload was as follows:
```
Found Aps 30
JSON payload length: 1949 bytes
Protobuf payload length: 966 bytes
```
It is already quite efficient. We have ~2 times fewer bytes with Protobuf.

But after adding a “s” before the int32 type for rssi, we got the following:
```
Found APs 30
JSON payload length: 1949 bytes
Protobuf payload length: 713 bytes
```
