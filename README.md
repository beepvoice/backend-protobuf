# backend-protobuf

Definitions of [protobufs](https://developers.google.com/protocol-buffers) used in Beep backend.

### Bite (bite.proto)

```proto
message Bite {
  bytes key = 1;
  uint64 start = 2;
  bytes data = 3;
}
```
