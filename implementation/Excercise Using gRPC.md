### Applying Using gRPC

Using the following `proto` file that defines computer orders, set up a gRPC server that accepts `OrderMessage`'s:
```proto
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

message Empty {

}

message OrderMessageList {
 repeated OrderMessage orders = 1;
}

service OrderService {
   rpc Create(OrderMessage) returns (OrderMessage);
   rpc Get(Empty) returns (OrderMessageList);
}
```
Feel free to use the [gRPC Demo Code](https://github.com/udacity/cd0309-message-passing-exercises/tree/master/lesson-3-implementing-message-passing/grpc-demo) as a starting point.

**Task List**

Set up and validate a gRPC server that can handle a `OrderMessage`.

Feel free to use the gRPC Demo Code as a starting point.
