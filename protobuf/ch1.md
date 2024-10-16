Serialized data size
---

The main reason why Protobuf is good at serializing data in a small number of bytes is that it is a binary format. In Protobuf,
additional structural elements such as curly braces, colons, and brackets, typically found in formats such as JSON, XML, and YAML, are absent. Instead, 
Protobuf data is represented simply as raw bytes.

Bitpacking is a method that compresses data into as few bits as possible. Notice that we are talking about bits and not bytes here. You can think of bitpacking as trying to put multiple pieces of data in the same number of bytes. Here is an example of bitpacking in Protobuf:

```
0a  -> 0101 00000
    -> 010 is 2 (length-delimited type like string)
    -> 1 is the field tag
```


Most of the integers in Protobuf are varints. Varints is short for variable-size integers and they map integers to different numbers of bytes. How this works is that the smaller values will get mapped to a smaller number of bytes and the bigger ones will get translated to a larger number of bytes. Let us see an example (decimal -> byte(s) in hexadecimal):
```
1 -> 01
128 -> 80 01
16,384 -> 80 80 01
```

Availability of data
---
So, as we saw, Protobuf serialized data is by default not human-readable. It is binary and it would take some extra effort or more tools to read. However, 
since Protobuf provides a way to serialize data to its own text format or to JSON, 
we can still have human-readable serialized data. This is nice for configuration files, test data, and so on.

Type safety
---

Protobuf lets us use types in a very explicit and safe way. We have an extensive set of types that we can use and that will let us ensure that our data is correct at compile time. Finally, 
we saw that by providing nested types referenced by their fully qualified names,
we can differentiate types with the same names and ensure that only certain correct values get set to fields.

Readability of schema
---
```
// A Duration represents a signed, fixed-length span of time represented
// as a count of seconds and fractions of seconds at nanosecond
// resolution. It is independent of any calendar and concepts like "day" or "month".
message Duration {
  // Signed seconds of the span of time. Must be from -315,576,000,000
  // to +315,576,000,000 inclusive. Note: these bounds are computed from:
  // 60 sec/min * 60 min/hr * 24 hr/day * 365.25 days/year * 10000 
  years
  int64 seconds;
  // Signed fractions of a second at nanosecond resolution of the span
  // of time. Durations less than one second are represented with a 0
  // `seconds` field and a positive or negative `nanos` field. For 
  durations
  // of one second or more, a non-zero value for the `nanos` field 
  must be
  // of the same sign as the `seconds` field. Must be from 
  -999,999,999
  // to +999,999,999 inclusive.
  int32 nanos;
}
```
