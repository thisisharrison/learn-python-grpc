# Learn gRPC

## Codegen

Generate the gRPC client and server interfaces from .proto service definition.

With `grpcio-tools`, you can

```shell
python -m grpc_tools.protoc -I<input folder> --python_out=<output folder for compiled proto files (pb2.py)> --grpc_python_out=<output folder for python code (pb2_grpc.py)> <proto message file>
```
