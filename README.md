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

### Screenshot of Queue Spike

![RabbitMQ Queue Spike](chart.png)

---

### Why is the total number of queued messages like that?

In my case, the queue temporarily reached **6 messages**.

Here’s why:

- I ran the publisher a bit more than once (each run sends 5 messages).
- Because the subscriber takes **1 second per message**, messages build up in the queue when the publisher is faster than the consumer.
- The graph shows:
  - A **flat line at 6** in "Queued messages", indicating the number of events waiting.
  - Then a drop as the subscriber processed messages one-by-one.