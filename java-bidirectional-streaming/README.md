# 🔄 gRPC Bidirectional Streaming — Java Implementation

This module provides a complete, code-heavy implementation of **all four gRPC communication patterns** in Java, with deep focus on **bidirectional streaming**. It includes multi-proto file organization, full server stubs, and clean client wrapper abstractions.

**Domain:** A real-time stock trading platform with live price feeds and order execution.

---

## 📂 Contents

| # | File | Description |
|---|------|-------------|
| 1 | [gRPC Streaming Patterns](1.gRPC%20Streaming%20Patterns.md) | Theory — all 4 gRPC patterns (unary, server-streaming, client-streaming, bidirectional) with sequence diagrams |
| 2 | [Bidirectional Streaming Implementation](2.Bidirectional%20Streaming%20Implementation.md) | Complete implementation — multi-proto files, Gradle config, server stubs, client wrappers, and runner code |

---

## 🎯 Learning Objectives

- Understand the **four gRPC communication patterns** and when to use each
- Write `.proto` service definitions with `stream` keyword for all streaming variants
- Implement **server-side `StreamObserver`** handlers for bidirectional streaming
- Build **client-side wrapper classes** that abstract raw gRPC stubs into clean APIs
- Handle **concurrent message flows** where client and server send independently
- Organize a multi-proto project with shared common types
- Run a complete bidirectional streaming system end-to-end

---

## ⚡ Quick Start

### Prerequisites

- **Java 11+** (JDK)
- **Gradle 7+**

### Build & Run

```bash
# Build everything
gradle build

# Terminal 1 — Start the trading server
gradle runServer

# Terminal 2 — Run the trading client (all patterns demo)
gradle runClient
```

---

## 🏗️ Architecture

```
┌──────────────────────┐                          ┌──────────────────────┐
│     Trading Client    │                          │    Trading Server     │
│                       │                          │                       │
│  ┌─────────────────┐  │    ──── Unary ─────►    │  ┌─────────────────┐  │
│  │ OrderClient     │──┼─────────────────────────┼──│ OrderServicer   │  │
│  │ (wrapper)       │  │    ◄─── Response ────    │  │                 │  │
│  └─────────────────┘  │                          │  └─────────────────┘  │
│                       │                          │                       │
│  ┌─────────────────┐  │    ◄── Price Stream ──   │  ┌─────────────────┐  │
│  │ MarketData      │──┼─────────────────────────┼──│ MarketData      │  │
│  │ Client (wrapper)│  │   Server Streaming       │  │ Servicer        │  │
│  └─────────────────┘  │                          │  └─────────────────┘  │
│                       │                          │                       │
│  ┌─────────────────┐  │    ── Order Batch ──►    │  ┌─────────────────┐  │
│  │ BatchOrder      │──┼─────────────────────────┼──│ BatchOrder      │  │
│  │ Client (wrapper)│  │   Client Streaming       │  │ Servicer        │  │
│  └─────────────────┘  │                          │                       │
│                       │                          │  └─────────────────┘  │
│  ┌─────────────────┐  │    ◄── Bidi Stream ──►   │  ┌─────────────────┐  │
│  │ LiveTrading     │──┼─────────────────────────┼──│ LiveTrading     │  │
│  │ Client (wrapper)│  │   Bidirectional          │  │ Servicer        │  │
│  └─────────────────┘  │                          │  └─────────────────┘  │
└──────────────────────┘                          └──────────────────────┘
```

---

## 📁 Project Structure

```
java-bidirectional-streaming/
├── build.gradle
├── settings.gradle
└── src/main/
    ├── proto/
    │   ├── common/
    │   │   └── types.proto                 ← shared primitives
    │   ├── market/
    │   │   └── market_data.proto           ← server streaming service
    │   └── trading/
    │       └── trading.proto               ← unary + client + bidi streaming
    └── java/com/example/trading/
        ├── server/
        │   ├── TradingServer.java          ← multi-service gRPC server
        │   ├── MarketDataServiceImpl.java  ← server streaming handler
        │   └── TradingServiceImpl.java     ← unary + client + bidi handlers
        └── client/
            ├── MarketDataClient.java       ← server streaming wrapper
            ├── TradingClient.java          ← unary + client streaming wrapper
            ├── LiveTradingClient.java      ← bidirectional streaming wrapper
            └── TradingApp.java             ← demo runner
```

---

## 🔑 The Four gRPC Patterns at a Glance

| Pattern | Proto Syntax | Client Sends | Server Sends | Use Case |
|---------|-------------|-------------|-------------|----------|
| **Unary** | `rpc Foo(Req) returns (Resp)` | 1 message | 1 message | Simple request/response |
| **Server Streaming** | `rpc Foo(Req) returns (stream Resp)` | 1 message | N messages | Live feeds, logs |
| **Client Streaming** | `rpc Foo(stream Req) returns (Resp)` | N messages | 1 message | Batch uploads |
| **Bidirectional** | `rpc Foo(stream Req) returns (stream Resp)` | N messages | N messages | Chat, live trading |

---

## 🔗 Related

- **← Theory Module** [`gRPC-basics/`](../gRPC-basics/) — Fundamentals of gRPC and protobuf
- **← Java Basics** [`java-implementation/`](../java-implementation/) — Introductory Java gRPC with unary RPCs
- **← Python Module** [`implementation/`](../implementation/) — Same concepts in Python
