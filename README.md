# backend-protobuf

Definitions of [protobufs](https://developers.google.com/protocol-buffers) used in Beep backend.

## Client (client.proto)

Defines a user client (user + device). Intended to be populated from auth token and convey the user through the pipeline.

| Field | Type | Description |
| ----- | ---- | ----------- |
| key | string | User's ID. (Unique to user) |
| client | string | User's device's ID. (Unique to user's device) |

---

## Bite (bite.proto)

A chunk of raw data. Doesn't necessarily have to be raw audio, could be text too in the case of ```backend-transcription```.

| Field | Type | Description |
| ----- | ---- | ----------- |
| key | string | Bite's key |
| client | uint64 | Bite's start time in Unix Epoch |
| data | bytes | Bite's raw audio data |
| client | Client | Client who submitted the Bite |

---

## Store (store.proto)

A request to store a Bite in ```backend-store```.

| Field | Type | Description |
| ----- | ---- | ----------- |
| type | string | Type of data to be stored. E.g. ```bite``` or ```transcription``` |
| bite | Bite | Bite to be stored |

---

## DataRequest

A request to get data from ```backend-store```. See more details in its README.

| Field | Type | Description |
| ----- | ---- | ----------- |
| key | string | The target key. |
| start | uint64 | The target data's start time in Unix Epoch time |
| type | string | The target data's type. E.g. ```bite``` or ```transcription``` |

---

## ScanRequest

A request to scan data from ```backend-store```. See more details in its README.

| Field | Type | Description |
| ----- | ---- | ----------- |
| key | string | The target key. |
| from | uint64 | Time to start scanning from in Unix Epoch time |
| to | uint64 | Time to scan to in Unix Epoch Time |
| type | string | The target data's type. E.g. ```bite``` or ```transcription``` |

---

## Response

A response, roughly follows the basics of a HTTP response (status code and message). Client can be left blank, usually when NATS is Requested from a HTTP request.

| Field | Type | Description |
| ----- | ---- | ----------- |
| code | uint32 | HTTP status code of response |
| message | string | Body of response. |
| client | Client | Client to respond to. |
