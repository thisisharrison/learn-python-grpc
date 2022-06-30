# Learn gRPC

## Codegen

Generate the gRPC client and server interfaces from .proto service definition.

With `grpcio-tools`, you can

```shell
python -m grpc_tools.protoc -I<input folder> --python_out=<output folder for compiled proto files (pb2.py)> --grpc_python_out=<output folder for python code (pb2_grpc.py)> <proto message file>
```

The generated code files are `_pb2.py` and `_pb2_grpc.py`. They contain:

- classes for the messages defined in `.proto`
- classes for the service defined in `.proto`
  - `<XXX>Stub`, which can be used by clients to invoke service's RPCs
  - `<XXX>Servicer`, which defines the interface for implementations of the service
- a function for the service defined in `.proto`
  - `add_<XXX>Servicer_to_server`, which adds a `<XXX>Servicer` to a grpc.Server

## Creating the server

1. Implement the servicer interface
2. Running a gRPC server to listen for requests from clients and transmit responses
