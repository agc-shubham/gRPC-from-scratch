# 📘 gRPC Basics — Theory & Concepts

This module covers the **foundational theory** behind gRPC, Protocol Buffers, and how they compare to REST. It is designed as a learning path that progresses from concepts → quizzes → exercise → solution.

---

## 📂 Contents

| # | File | Description |
|---|------|-------------|
| 1 | [Using gRPC](1.using-gRPC.md) | Core concepts — what gRPC is, HTTP/2 advantages, Protocol Buffers, services, and use cases |
| 2 | [Quizzes Using gRPC](2.Quizzes%20Using%20gRPC.md) | Self-assessment quiz matching gRPC properties to definitions |
| 3 | [Exercise Planning for gRPC](3.Exercise%20Planning%20for%20gRPC.md) | Hands-on exercise: design a protobuf message and service for a computer ordering system |
| 4 | [Solution Planning for gRPC](4.Solution%20Planning%20for%20gRPC.md) | Walkthrough of simple and advanced solutions using enums and strict typing |

---

## 🎯 Learning Objectives

By completing this module you will be able to:

- Explain what gRPC is and why Google created it
- Describe the performance advantages of HTTP/2 and binary data over HTTP/1.1 and JSON
- Define **Protocol Buffer** messages with typed fields, field numbers, enums, and repeated fields
- Define **Protobuf Services** that declare strict RPC interfaces
- Compare and contrast gRPC vs REST trade-offs (speed, structure, flexibility, adoption)
- Identify real-world use cases: microservices, mobile devices, and high-throughput systems
- Design a complete `.proto` file for a domain-specific service (computer orders)

---

## 📝 Key Concepts at a Glance

### What is gRPC?

- A **Remote Procedure Call** framework developed by Google (2015)
- Language-agnostic, leveraging **HTTP/2** and **Protocol Buffers**
- Faster than REST out-of-the-box due to binary serialization and multiplexed connections

### Protocol Buffers (Protobuf)

- Structured, typed, binary-serialized message format (alternative to JSON/YAML)
- Backward & forward compatible — unknown fields are safely ignored
- Defined in `.proto` files using `proto3` syntax

```protobuf
message Item {
  string name = 1;
  string brand_name = 2;
  int32 id = 3;
  float weight = 4;
}
```

### Protobuf Services

```protobuf
service ItemService {
    rpc Create(ItemMessage) returns (ItemMessage);
}
```

### gRPC vs REST

| Aspect | gRPC | REST |
|--------|------|------|
| Data Format | Binary (protobuf) | Text (JSON/XML) |
| Transport | HTTP/2 | HTTP/1.1 or HTTP/2 |
| Type Safety | Enforced | Not enforced |
| Adoption | Growing | Widespread |
| Flexibility | Less flexible | Highly flexible |
| Performance | Faster | Slower (comparatively) |

---

## 📖 Suggested Reading Order

1. Start with **`1.using-gRPC.md`** to build foundational knowledge
2. Test yourself with **`2.Quizzes Using gRPC.md`**
3. Attempt the exercise in **`3.Exercise Planning for gRPC.md`** before looking at the solution
4. Review and compare your solution with **`4.Solution Planning for gRPC.md`**

---

## 🔗 Related

- **Next Module →** [`implementation/`](../implementation/) — Hands-on Python implementation with `grpcio` and `grpcio-tools`
