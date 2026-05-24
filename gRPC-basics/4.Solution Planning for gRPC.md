### My Solution
[video](https://www.youtube.com/watch?v=oaHCucGGhPU)
### Simple Solution

From our previous exercise, we know that a possible way to structure an Order resource looks like this:
### ***JSON***
```json
{
    "order_id": <order_id: str>,
    "created_by": <user_id: str>,
    "status": <status_enum: str>,
    "created_at": <isoformat_timestamp: str>,
    "equipment": [
        <equipment: str>
    ]
}
```
### Protobuf Message - Simple Solution
```protobuf
message OrderMessage {
  string order_id = 1;
  string created_by = 2;
  string status = 3;
  string created_at = 4;
  repeated string equipment = 5;
}
```
We are essentially mapping the JSON message into a Protobuf message. This may seem a little trivial -- the only benefit we get is that the fields have enforced typing of strings.

With JSON, typing isn't enforced and we need application code to validate the type. For example, if we can pass `order_id` as an int instead of a string in JSON messages but protobuf messages will raise an error.
### Service

Since our `OrderMessage` is used as both the request and response, our service can be easily defined as:
```protobuf
service OrderService {
    rpc Create(OrderMessage) returns (OrderMessage);
}
```
### Create an Even More Amazing Protobuf Message

[video](https://www.youtube.com/watch?v=DbCbSJUhiQE)
### Protobuf Message - Better Solution
**Valid Strings in JSON**

When we look at the fields captured in our object, what exactly constitutes a valid `status` field? When implemented into REST, we often write application code to check this value in the JSON message to ensure that it is one of `Queued`, `Processing`, `Completed`, and Fa`iled.

**Valid Strings in Protobuf**

We can leverage protobuf so that our messages have built-in validation and we don't have to write additional code to validate the messages. The following is an example of using enumerated values to build a strict, structured message that makes our messages easy to process.

**Protobuf Message Example**
```protobuf
message OrderMessage {
 enum Status {
    Queued = 0;
    Processing = 1;
    Completed = 2;
    Failed = 3;
  }

  enum Equipment {
    Keyboard = 0;
    Mouse = 1;
    Webcam = 2;
    Monitor = 3;
  }

  string id = 1;
  string created_by = 2;
  Status status = 3;
  string created_at = 4;
  repeated Equipment equipment = 5;
}
```
>    Instead of passing strings to the `status` and `equipment`, we enforce that only one of the `Status` and `Equipment` `enum`'s are valid inputs.

**Comparisons**

Overall, protobuf messages are more strict and allow you to have built-in validations.

RESTful APIs using JSON are deliberately very flexible, and those who want to add more data validation into their applications rely on 3rd party libraries. For example, Python applications often use tools like `marshmallow` to validate data by performing validations, such as ensuring that the value in a field is a string.