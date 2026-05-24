# 🛠️ gRPC Implementation — Hands-On with Python

This module walks through the **practical implementation** of a gRPC client and server in Python. Building on the concepts from [`gRPC-basics/`](../gRPC-basics/), you will generate code from `.proto` files, build a server, and create client scripts to interact with it.

---

## 📂 Contents

| # | File | Description |
|---|------|-------------|
| 1 | [Using gRPC](1.Using%20gRPC.md) | Step-by-step guide to implementing gRPC with Python — proto file → code generation → server/client |
| 2 | [Exercise Using gRPC](2.Excercise%20Using%20gRPC.md) | Exercise: build a gRPC server for a computer ordering service using the `OrderMessage` proto |
| 3 | [Solution Using gRPC](3.Solution%20Using%20gRPC.md) | Complete solution walkthrough with server (`main.py`), writer (`writer.py`), and getter (`getter.py`) |

---

## 🎯 Learning Objectives

By completing this module you will be able to:

- Install and use `grpcio` and `grpcio-tools` in a Python environment
- Write a `.proto` file with messages, enums, and service definitions
- Generate Python gRPC stubs using `grpc_tools.protoc`
- Implement a **gRPC server** with custom service logic
- Build **gRPC clients** that invoke remote procedures as local method calls
- Validate type safety by observing errors when incorrect types are passed

---

## ⚡ Quick Start

### Prerequisites

```bash
pip install grpcio grpcio-tools
```

### Workflow

The implementation follows a 3-step process:

```
┌──────────────┐     grpcio-tools     ┌──────────────────┐     grpcio     ┌──────────────────┐
│  .proto file │  ──────────────────► │  Generated Python │ ────────────► │  Client & Server │
│  (Definitions)│                     │  _pb2.py files    │               │  Application Code│
└──────────────┘                      └──────────────────┘               └──────────────────┘
```

**Step 1** — Define your protobuf messages and services in a `.proto` file:

```protobuf
syntax = "proto3";

message OrderMessage {
  enum Status { QUEUED = 0; PROCESSING = 1; COMPLETED = 2; FAILED = 3; }
  enum Equipment { KEYBOARD = 0; MOUSE = 1; WEBCAM = 2; MONITOR = 3; }
  
  string id = 1;
  string created_by = 2;
  Status status = 3;
  string created_at = 4;
  repeated Equipment equipment = 5;
}

service OrderService {
  rpc Create(OrderMessage) returns (OrderMessage);
  rpc Get(Empty) returns (OrderMessageList);
}
```

**Step 2** — Generate Python gRPC files:

```bash
python -m grpc_tools.protoc -I./ --python_out=./ --grpc_python_out=./ computer_orders.proto
```

This produces:
- `computer_orders_pb2.py` — message classes
- `computer_orders_pb2_grpc.py` — service stubs

> ⚠️ **Do not edit** the generated `_pb2.py` and `_pb2_grpc.py` files — they contain auto-generated code.

**Step 3** — Import and use in your application:

```python
import grpc
import computer_orders_pb2
import computer_orders_pb2_grpc
```

### Running

```bash
# Terminal 1 — Start the gRPC server
python main.py

# Terminal 2 — Send an order (Create)
python writer.py

# Terminal 3 — Retrieve orders (Get)
python getter.py
```

---

## 🔑 Key Files in the Solution

| File | Role |
|------|------|
| `computer_orders.proto` | Protobuf definitions (messages + services) |
| `computer_orders_pb2.py` | Auto-generated message classes |
| `computer_orders_pb2_grpc.py` | Auto-generated service stubs |
| `main.py` | gRPC **server** — implements `OrderServicer` |
| `writer.py` | gRPC **client** — demonstrates `Create` RPC |
| `getter.py` | gRPC **client** — demonstrates `Get` RPC |

---

## 📖 Key Terms

| Term | Definition |
|------|-----------|
| `grpcio` | Python library to run gRPC client and server code |
| `grpcio-tools` | Python library to generate definition code from `.proto` files |
| `_pb2.py` | Generated file containing protobuf message class definitions |
| `_pb2_grpc.py` | Generated file containing gRPC service stubs |

---

## 🔗 Resources

- [gRPC Demo Source Code (Starter)](https://github.com/udacity/cd0309-message-passing-exercises/tree/master/lesson-3-implementing-message-passing/grpc-demo)
- [gRPC Solution Code](https://github.com/udacity/cd0309-message-passing-exercises/tree/master/lesson-3-implementing-message-passing/grpc-solution)
- [gRPC Used in Netflix Tools](https://netflixtechblog.com/evolution-of-netflix-conductor-16600be36bca)
- [Dropbox Migration to gRPC](https://dropbox.tech/infrastructure/courier-dropbox-migration-to-grpc)

---

## 🔗 Related

- **← Previous Module** [`gRPC-basics/`](../gRPC-basics/) — Theory, concepts, and protobuf design exercises
