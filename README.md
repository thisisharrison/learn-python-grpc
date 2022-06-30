# Learn gRPC

Going through the examples from [gRPC Documentation](https://grpc.io/docs/languages/python/).

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
- a registration function for the service defined in `.proto`
  - `add_<XXX>Servicer_to_server`, which adds a `<XXX>Servicer` to a grpc.Server
  - Registers a `Servicer` object implementing it on a `grpc.Server` object, so that the server can route queries to the respective servicer

## Creating the server

1. Implement the `Servicer` class interface
2. Running a gRPC server to listen for requests from clients and transmit responses
3. Connect the `Servicer` with the `grpc.Server` with the `add_<XXX>Servicer_to_server` registration function.

Side note: Comments associated with code elements in the .proto file appear as docstrings in the generated python code.

## Creating the client

1. `Stub` class has a constructor that takes a `grpc.Channel` object. Each method in the service, the initializer adds attribute to the stub object with the same name. The value of that attribute will be callable objects of

- `UnaryUnaryMultiCallable` = Simple RPC
- `UnaryStreamMultiCallable` = Response-streaming RPC
- `StreamUnaryMultiCallable` = Request-streaming RPC
- `StreamStreamMultiCallable` = Bidirectional streaming RPC
