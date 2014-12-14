protobuf2json-c [![BS][BSI]][BSURL] [![CS][CSI]][CSURL]
=======================================================

This is `protobuf2json-c`, pure C implementation of the [Google Protocol Buffers] to/from JSON converter.

[BSI]: https://secure.travis-ci.org/Sannis/protobuf2json-c.png?branch=master
[BSURL]: http://travis-ci.org/Sannis/protobuf2json-c

[CSI]: https://coveralls.io/repos/Sannis/protobuf2json-c/badge.png
[CSURL]: https://coveralls.io/r/Sannis/protobuf2json-c

[Google Protocol Buffers]: https://developers.google.com/protocol-buffers/

Building
--------

`protobuf2json-c` requires a C compiler, [protobuf-c 1.0.0][] and [jansson 2.7][] to be installed.
If building from a git checkout, the `autotools` (`autoconf`, `automake`, `libtool`) must also be installed,
and the build system must be generated by running the `autogen.sh` script:

    ./autogen.sh && ./configure && make && make install

[protobuf-c]: https://github.com/protobuf-c/protobuf-c
[jansson]: https://github.com/akheron/jansson

API
---

`protobuf2json-c` piblic API containt 6 functions:
3 for Protobuf to JSON conversion and 3 for JSON to Protobuf conversion.
They uses `json_t` object, `char *` C-string or file for JSON.

Protobuf to JSON conversion functions:

```
int protobuf2json_object(
  ProtobufCMessage *protobuf_message,
  json_t **json_object,
  char *error_string,
  size_t error_size
);
```

```
int protobuf2json_string(
  ProtobufCMessage *protobuf_message,
  size_t json_flags,
  char **json_string,
  char *error_string,
  size_t error_size
);
```

```
int protobuf2json_file(
  ProtobufCMessage *protobuf_message,
  size_t json_flags,
  char *json_file,
  char *fopen_mode,
  char *error_string,
  size_t error_size
);
```

JSON to Protobuf conversion functions:

```
int json2protobuf_object(
  json_t *json_object,
  const ProtobufCMessageDescriptor *protobuf_message_descriptor,
  ProtobufCMessage **protobuf_message,
  char *error_string,
  size_t error_size
);
```

```
int json2protobuf_string(
  char *json_string,
  size_t json_flags,
  const ProtobufCMessageDescriptor *protobuf_message_descriptor,
  ProtobufCMessage **protobuf_message,
  char *error_string,
  size_t error_size
);
```

```
int json2protobuf_file(
  char *json_file,
  size_t json_flags,
  const ProtobufCMessageDescriptor *protobuf_message_descriptor,
  ProtobufCMessage **protobuf_message,
  char *error_string,
  size_t error_size
);
```

Each of them have `error_string` and `error_size` arguments used to pass error description from `protobuf2json-c` functions.
You can pass `NULL` and `0` to avoid setting error description.


Credits
-------

`protobuf2json-c` based on code from:
 - https://github.com/wickedck/protobuf-to-json
 - https://github.com/renenglish/pb2json
 - https://github.com/michaelstorm/Tangent

License
-------

MIT license. See license text in file [LICENSE](https://github.com/Sannis/protobuf2json-c/blob/master/LICENSE).
