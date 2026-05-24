## Using gRPC

News of our computer ordering service has made its way to other departments in the organization. After using the service to place multiple orders, some data scientists have decided that they want to perform analysis on the financial department's computer orders! We don't need to understand how their models work, but we need to set up a way to retrieve the data. Their team leverages gRPC for its strong performance and strict data structuring to run their models.

For your reference, the following is the sample protobuf message that was introduced in the lesson:
```protobuf
syntax = "proto3";


message Item {
  string name = 1;
  string brand_name = 2;
  int32 id = 3;
  float weight = 4;
}

Service ItemService {
    rpc Create(ItemMessage) returns (ItemMessage)
}
```
### **Task List**

Plan for the gRPC service by creating the protobuf message and computer ordering service.

To customize the computer orders, we want to allow users to specify the equipment that they want on the computer. An order should also include the user who created the order, the status of the order, and the time an order was placed.

Using the proto3 syntax, create the message and services for our computer ordering application. You may find it useful to use your previous JSON solution as a starting point and reference the protobuf documentation.
