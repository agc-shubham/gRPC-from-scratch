# 🚀 gRPC from Scratch

A comprehensive, self-paced learning resource for understanding and implementing **gRPC** (Google Remote Procedure Calls) with **Python** and **Java**. This repository takes you from core concepts to fully working client-server applications in both languages.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Project Structure](#-project-structure)
- [Modules](#-modules)
  - [Module 1: gRPC Basics](#module-1-grpc-basics--theory--concepts)
  - [Module 2: Python Implementation](#module-2-python-implementation--hands-on-with-python)
  - [Module 3: Java Implementation](#module-3-java-implementation--hands-on-with-java)
- [Getting Started](#-getting-started)
- [How gRPC Works](#-how-grpc-works)
- [Key Concepts](#-key-concepts)
- [Resources](#-resources)

---

## 🌟 Overview

gRPC is a high-performance, language-agnostic RPC framework developed by Google in 2015. It uses **Protocol Buffers** (protobuf) for efficient binary serialization and **HTTP/2** for fast, multiplexed transport.

This repository covers:

- ✅ **What** gRPC is and how it compares to REST
- ✅ **Why** gRPC is faster (HTTP/2, binary data, structured typing)
- ✅ **How** to design protobuf messages and services
- ✅ **How** to implement a gRPC server and client in **Python**
- ✅ **How** to implement a gRPC server and client in **Java**
- ✅ Hands-on exercises with detailed solutions in both languages
- ✅ Side-by-side **Python ↔ Java** comparisons

---

## 📁 Project Structure

```
gRPC-from-scratch/
│
├── README.md                          # ← You are here
├── protobut-to-python-code.jpg        # Diagram: protobuf → grpcio-tools → Python code
│
├── gRPC-basics/                       # Module 1: Theory & Concepts
│   ├── README.md
│   ├── 1.using-gRPC.md               # Core concepts & fundamentals
│   ├── 2.Quizzes Using gRPC.md       # Self-assessment quiz
│   ├── 3.Exercise Planning for gRPC.md  # Design exercise
│   └── 4.Solution Planning for gRPC.md  # Solution walkthrough
│
├── implementation/                    # Module 2: Hands-On Python
│   ├── README.md
│   ├── 1.Using gRPC.md               # Step-by-step Python implementation guide
│   ├── 2.Excercise Using gRPC.md     # Build a gRPC server exercise
│   └── 3.Solution Using gRPC.md      # Complete solution with server & clients
│
└── java-implementation/               # Module 3: Hands-On Java
    ├── README.md
    ├── 1.Using gRPC.md               # Step-by-step Java implementation guide
    ├── 2.Exercise Using gRPC.md      # Build a gRPC server exercise
    ├── 3.Solution Using gRPC.md      # Complete solution with server & clients
    └── 4.Advanced Multi-Proto Builds  # Multi-proto imports & e-commerce example
        with Gradle.md
```

---

## 📚 Modules

### Module 1: gRPC Basics — Theory & Concepts

📂 [`gRPC-basics/`](gRPC-basics/)

Builds foundational knowledge of gRPC, Protocol Buffers, and HTTP/2. Follows a structured learning path:

| # | Topic | What You'll Learn |
|---|-------|-------------------|
| 1 | **Using gRPC** | What gRPC is, HTTP/2, protobuf messages & services, gRPC vs REST |
| 2 | **Quiz** | Test your understanding of gRPC properties and comparisons |
| 3 | **Exercise** | Design a protobuf message and service for a computer ordering system |
| 4 | **Solution** | Simple solution → advanced solution using enums for strict validation |

**Key takeaway:** Learn to design `.proto` files that enforce type safety and provide built-in validation through enums and structured typing.

---

### Module 2: Python Implementation — Hands-On with Python

📂 [`implementation/`](implementation/)

Translates theory into working code. Covers the complete gRPC development workflow in Python:

| # | Topic | What You'll Learn |
|---|-------|-------------------|
| 1 | **Using gRPC** | Install `grpcio`/`grpcio-tools`, generate stubs, build server & client |
| 2 | **Exercise** | Implement a gRPC server for the computer ordering service |
| 3 | **Solution** | Full server (`main.py`), writer client (`writer.py`), getter client (`getter.py`) |

**Key takeaway:** Master the 3-step gRPC workflow — define `.proto` → generate Python stubs → implement application logic.

---

### Module 3: Java Implementation — Hands-On with Java

📂 [`java-implementation/`](java-implementation/)

Re-implements the same exercises in Java, showcasing how gRPC's language-agnostic design works across different ecosystems:

| # | Topic | What You'll Learn |
|---|-------|-------------------|
| 1 | **Using gRPC** | Gradle setup, protobuf plugin, Java code generation, server & client |
| 2 | **Exercise** | Build the same `OrderService` gRPC server in Java |
| 3 | **Solution** | Full server (`OrderServer.java`), writer (`OrderWriter.java`), getter (`OrderGetter.java`) |
| 4 | **Advanced Multi-Proto** | Multiple proto files with imports, shared common types, cross-service references — e-commerce platform example |

**Key takeaway:** Java's compile-time type system + protobuf catches errors **before code runs**. The Builder pattern and `StreamObserver` are Java's idiomatic gRPC patterns. For large projects, proto imports and shared common files keep definitions DRY.

---

## 🏁 Getting Started

### Prerequisites

| Language | Requirements |
|----------|--------------|
| **Python** | Python 3.7+, pip |
| **Java** | JDK 11+, Gradle 7+ (or Maven 3.6+) |

### Installation

**Python:**
```bash
pip install grpcio grpcio-tools
```

**Java (Gradle):** Add to `build.gradle`:
```groovy
dependencies {
    implementation 'io.grpc:grpc-netty-shaded:1.68.0'
    implementation 'io.grpc:grpc-protobuf:1.68.0'
    implementation 'io.grpc:grpc-stub:1.68.0'
    compileOnly 'javax.annotation:javax.annotation-api:1.3.2'
}
```

### The 3-Step gRPC Workflow (Same for Both Languages)

```
  ┌─────────────────┐      protoc compiler      ┌─────────────────────┐      language       ┌─────────────────┐
  │   Definitions    │  ───────────────────────► │   Generated Code    │  ──────────────►   │  Client/Server  │
  │   (.proto file)  │  (grpcio-tools / Gradle)  │ (Python or Java)    │   import & use     │  Application    │
  └─────────────────┘                            └─────────────────────┘                    └─────────────────┘
```

**Step 1** — Define messages and services in a `.proto` file  
**Step 2** — Generate code (Python: `grpc_tools.protoc` CLI / Java: `gradle build` with plugin)  
**Step 3** — Import generated files and implement your business logic

### Running the Examples

**Python:**
```bash
# Terminal 1 — Start the server
python main.py

# Terminal 2 — Create an order
python writer.py

# Terminal 3 — Retrieve all orders
python getter.py
```

**Java:**
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

## ⚙️ How gRPC Works

### Architecture

```
  ┌──────────────┐                           ┌──────────────┐
  │  gRPC Client │ ────── HTTP/2 ──────────► │  gRPC Server │
  │              │ ◄───── Binary Data ─────── │              │
  │  (stub)      │    Protobuf Messages       │  (servicer)  │
  └──────────────┘                           └──────────────┘
```

1. **Client** calls a method on a local stub as if it were a regular function
2. The stub **serializes** the request into a protobuf binary message
3. The message is sent over **HTTP/2** to the server
4. The server **deserializes** the message, executes logic, and sends back a response
5. The client receives and deserializes the response

### Why gRPC is Fast

| Feature | Benefit |
|---------|---------|
| **HTTP/2** | Multiplexed connections, reduced overhead |
| **Binary serialization** | Smaller payloads than JSON/XML |
| **Structured data** | No runtime parsing — decode directly into typed objects |
| **Connection reuse** | Single persistent connection between client and server |

---

## 🔑 Key Concepts

### gRPC vs REST

| Aspect | gRPC | REST |
|--------|------|------|
| **Data format** | Binary (protobuf) | Text (JSON/XML) |
| **Transport** | HTTP/2 | HTTP/1.1 or HTTP/2 |
| **Type safety** | Enforced at compile time | Not enforced |
| **Code generation** | Automatic stubs | Manual or via OpenAPI |
| **Adoption** | Growing rapidly | Industry standard |
| **Flexibility** | Strict contracts | Highly flexible |
| **Performance** | ⚡ Faster | Comparatively slower |

### Protobuf Message Example

```protobuf
syntax = "proto3";

message OrderMessage {
  enum Status {
    QUEUED = 0;
    PROCESSING = 1;
    COMPLETED = 2;
    FAILED = 3;
  }

  enum Equipment {
    KEYBOARD = 0;
    MOUSE = 1;
    WEBCAM = 2;
    MONITOR = 3;
  }

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

### Glossary

| Term | Definition |
|------|-----------|
| **gRPC** | Language-agnostic RPC framework using protocol buffers for strict interfaces |
| **HTTP/2** | Secure, performant HTTP protocol with multiplexing and binary framing |
| **Protocol Buffers** | Binary serialization format for structured data, optimized for size and speed |
| **protobuf** | Short for Protocol Buffers |
| **grpcio** | Python library to run gRPC client and server code |
| **grpcio-tools** | Python library to generate code from `.proto` definitions |
| **Stub** | Auto-generated client code that makes remote calls appear local |
| **Servicer** | Server-side implementation of gRPC service methods |

---

## 🔗 Resources

### Official Documentation
- [gRPC Official Site](https://grpc.io/)
- [Protocol Buffers — Proto3 Language Guide](https://protobuf.dev/programming-guides/proto3/)
- [gRPC Python Quick Start](https://grpc.io/docs/languages/python/quickstart/)
- [gRPC Java Quick Start](https://grpc.io/docs/languages/java/quickstart/)
- [gRPC Java Examples (GitHub)](https://github.com/grpc/grpc-java/tree/master/examples)

### Starter & Solution Code
- [gRPC Demo (Starter Code)](https://github.com/udacity/cd0309-message-passing-exercises/tree/master/lesson-3-implementing-message-passing/grpc-demo)
- [gRPC Solution Code](https://github.com/udacity/cd0309-message-passing-exercises/tree/master/lesson-3-implementing-message-passing/grpc-solution)

### Industry Case Studies
- [gRPC at Netflix](https://netflixtechblog.com/evolution-of-netflix-conductor-16600be36bca)
- [Dropbox Migration to gRPC](https://dropbox.tech/infrastructure/courier-dropbox-migration-to-grpc)

---

## 📖 Suggested Learning Path

```
 1. gRPC Basics: Core Concepts          ──►  gRPC-basics/1.using-gRPC.md
 2. Quiz: Test Your Knowledge            ──►  gRPC-basics/2.Quizzes Using gRPC.md
 3. Exercise: Design a Protobuf          ──►  gRPC-basics/3.Exercise Planning for gRPC.md
 4. Solution: Review Protobuf Design     ──►  gRPC-basics/4.Solution Planning for gRPC.md
 ── Python Track ──────────────────────────────────────────────────────────
 5. Python Implementation Guide          ──►  implementation/1.Using gRPC.md
 6. Exercise: Build a gRPC Server (Py)   ──►  implementation/2.Excercise Using gRPC.md
 7. Solution: Complete Python Impl.      ──►  implementation/3.Solution Using gRPC.md
 ── Java Track ────────────────────────────────────────────────────────────
 8. Java Implementation Guide            ──►  java-implementation/1.Using gRPC.md
 9. Exercise: Build a gRPC Server (Java) ──►  java-implementation/2.Exercise Using gRPC.md
10. Solution: Complete Java Impl.        ──►  java-implementation/3.Solution Using gRPC.md
11. Advanced: Multi-Proto Builds         ──►  java-implementation/4.Advanced Multi-Proto Builds with Gradle.md
```

> **Tip:** Steps 1–4 are shared theory. Then choose the **Python Track** (5–7), the **Java Track** (8–11), or do both to compare!

---


