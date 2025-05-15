## How much data is sent in one run?

In one run, the publisher sends **5 events** to the RabbitMQ message broker.

Each event is an instance of the following struct:

```rust
pub struct UserCreatedEventMessage {
    pub user_id: String,
    pub user_name: String,
}
```

## Explain the meaning of the connection URL.
amqp://guest:guest@localhost:5672

- This URL defines how the publisher connects to the RabbitMQ server using the AMQP protocol.

amqp://
- Specifies that the connection will use the Advanced Message Queuing Protocol (AMQP).

guest : guest
- These are the login credentials:
- The first guest is the username
- The second guest is the password
- These are default credentials provided by RabbitMQ.

localhost:5672
- Indicates the host and port:
- localhost means RabbitMQ is running on the same machine.

5672 is the default port for AMQP protocol connections.

This tells the application to connect to a RabbitMQ server running locally, authenticate as guest, and use the standard messaging port.