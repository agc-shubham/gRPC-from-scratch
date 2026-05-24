# ☕ gRPC Implementation — Hands-On with Java

This module walks through the **practical implementation** of a gRPC client and server in Java. Building on the concepts from [`gRPC-basics/`](../gRPC-basics/) and paralleling the Python module in [`implementation/`](../implementation/), you will set up a Gradle project, generate Java code from `.proto` files, build a server, and create client applications.

---

## 📂 Contents

| # | File | Description |
|---|------|-------------|
| 1 | [Using gRPC](1.Using%20gRPC.md) | Step-by-step guide: Gradle setup → proto file → code generation → server & client with full code |
| 2 | [Exercise Using gRPC](2.Exercise%20Using%20gRPC.md) | Exercise: build a Java gRPC server for the computer ordering service with `OrderMessage` |
| 3 | [Solution Using gRPC](3.Solution%20Using%20gRPC.md) | Complete solution: `OrderServer.java`, `OrderWriter.java`, `OrderGetter.java` with expected outputs |
| 4 | [Advanced Multi-Proto Builds](4.Advanced%20Multi-Proto%20Builds%20with%20Gradle.md) | Multi-proto imports, shared common types, cross-service references — full e-commerce platform example |

---

## 🎯 Learning Objectives

By completing this module you will be able to:

- Set up a Java gRPC project with **Gradle** (or Maven) and the protobuf compiler plugin
- Write `.proto` files with Java-specific options (`java_package`, `java_outer_classname`)
- Auto-generate Java stubs and message classes using `gradle build`
- Implement a **gRPC server** by extending `ServiceImplBase` and using `StreamObserver`
- Build **gRPC clients** using `ManagedChannel` and blocking stubs
- Construct protobuf messages using the **Builder pattern**
- Compare and contrast the Python and Java gRPC development workflows
- Organize **multi-proto projects** with shared common types and cross-service imports
- Host **multiple gRPC services** on a single server

---

## ⚡ Quick Start

### Prerequisites

- **Java 11+** (JDK)
- **Gradle 7+** (or Maven 3.6+)

### Dependencies (Gradle)

```groovy
dependencies {
    implementation 'io.grpc:grpc-netty-shaded:1.68.0'
    implementation 'io.grpc:grpc-protobuf:1.68.0'
    implementation 'io.grpc:grpc-stub:1.68.0'
    compileOnly 'javax.annotation:javax.annotation-api:1.3.2'
}
```

### Workflow

```
  .proto file   ──►   gradle build   ──►   Generated Java   ──►   Server & Clients
  (Definitions)       (auto protoc)        (Proto + Grpc)         (Application Code)
```

### Running

```bash
# Build
gradle build

# Terminal 1 — Start the server
gradle runServer

# Terminal 2 — Create an order
gradle runWriter

# Terminal 3 — Retrieve all orders
gradle runGetter
```

---

## 🔑 Key Files in the Solution

| File | Role |
|------|------|
| `computer_orders.proto` | Protobuf definitions (messages + services) |
| `OrderProto.java` | Auto-generated message classes (Builder pattern) |
| `OrderServiceGrpc.java` | Auto-generated service stubs and base class |
| `OrderServer.java` | gRPC **server** — implements `OrderServiceImpl` |
| `OrderWriter.java` | gRPC **client** — demonstrates `Create` RPC |
| `OrderGetter.java` | gRPC **client** — demonstrates `Get` RPC |

---

## 🔄 Python ↔ Java Comparison

| Aspect | Python | Java |
|--------|--------|------|
| Package manager | `pip` | Gradle / Maven |
| Code generation | Manual CLI command | Automatic build plugin |
| Message creation | Constructor kwargs | Builder pattern |
| Server response | `return message` | `StreamObserver.onNext()` + `.onCompleted()` |
| Type enforcement | Runtime errors | **Compile-time errors** ✅ |
| Boilerplate | Less | More (but more explicit) |

---

## 📖 Key Terms

| Term | Definition |
|------|-----------|
| `grpc-netty-shaded` | Java gRPC transport layer based on Netty HTTP/2 |
| `grpc-protobuf` | Bridges protobuf and gRPC for Java |
| `grpc-stub` | Provides generated stub classes for clients |
| `StreamObserver` | Interface for handling gRPC responses asynchronously |
| `ManagedChannel` | Client-side channel managing the HTTP/2 connection |
| `BlockingStub` | Synchronous client stub that blocks until response |

---

## 🔗 Resources

- [gRPC Java Quick Start](https://grpc.io/docs/languages/java/quickstart/)
- [gRPC Java GitHub Examples](https://github.com/grpc/grpc-java/tree/master/examples)
- [Protobuf Java Tutorial](https://protobuf.dev/getting-started/javatutorial/)

---

## 🔗 Related

- **← Theory Module** [`gRPC-basics/`](../gRPC-basics/) — Concepts, quizzes, and protobuf design
- **← Python Module** [`implementation/`](../implementation/) — Same exercises implemented in Python
