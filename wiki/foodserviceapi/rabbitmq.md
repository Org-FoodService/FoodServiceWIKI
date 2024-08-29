# 📦 RabbitMQ

#### RabbitMQ Integration in FoodServiceAPI

**Overview**

In FoodServiceAPI, RabbitMQ is used to facilitate real-time communication and messaging between different components of the application. This integration ensures that order updates, notifications, and other critical events are seamlessly transmitted across the system, enhancing the overall functionality and scalability of the application.

**Key Components**

1.  **RabbitMQ Overview**

    * **What is RabbitMQ?** RabbitMQ is a robust open-source message broker that enables applications to communicate asynchronously through message queues. It supports a variety of messaging protocols and patterns, making it a versatile choice for distributed systems.
    * **How RabbitMQ Works:** RabbitMQ works by receiving messages from producers (senders) and routing them to the appropriate queues. Consumers (receivers) then process the messages from these queues. This decoupling of message production and consumption allows for more scalable and resilient systems.


2.  **Accessing RabbitMQ Interface**

    To monitor and manage the messages and queues, RabbitMQ provides a user-friendly web interface. Here’s how you can access and use it:

    1. **Accessing the RabbitMQ Management Interface:**
       * Open your web browser and navigate to http://localhost:15672.
       * This URL directs you to the RabbitMQ management interface, where you can view queues, exchanges, bindings, and more.
    2.  **Login Credentials:**

        * **Username:** `guest`
        * **Password:** `guest`

        Use these credentials to log in to the RabbitMQ management interface.
    3. **Interface Overview:**
       * **Queues:** View and manage the queues where your messages are being sent. You can see message statistics, purge queues, or even send test messages.
       * **Exchanges:** Manage message routing between producers and queues. Exchanges direct messages to appropriate queues based on routing keys.
       * **Bindings:** Manage the connections between exchanges and queues.
       * **Admin:** Manage users, permissions, and virtual hosts.
    4.  **Monitoring and Troubleshooting:**

        * The RabbitMQ interface provides detailed insights into the state of your message broker. You can monitor message flow, view logs, and troubleshoot any issues that arise.



    **Docker Engine Requirement**

    Running RabbitMQ with Docker in FoodServiceAPI requires Docker to be installed and running on the host machine. Ensure Docker is properly configured and accessible for seamless integration with the RabbitMQ setup. The application will not have full messaging capabilities without it, which may affect certain features dependent on message queues.


3.  **Utilizing RabbitMQ in FoodServiceAPI**

    * **Message Queues:**
      * **Order Queue:** This queue handles messages related to order creation, updates, and status changes. Whenever an order is placed or updated, a message is sent to the `order_queue`, ensuring that all relevant parties (e.g., kitchen staff, delivery personnel, customers) are notified in real time.
      * **Notification Queue:** This queue is responsible for sending notifications to users about the status of their orders. As orders move through various stages (e.g., "Preparing," "Ready for Delivery," "Delivered"), notifications are triggered and sent through this queue.
    * **Outbox Pattern:** The Outbox pattern is implemented to ensure reliable message delivery. Before a message is sent to RabbitMQ, it is first stored in an "outbox" table in the database. Once the transaction is committed, the message is then published to the RabbitMQ queue, guaranteeing that messages are not lost in case of system failures.


4.  **RabbitMQDockerManager**

    * **Docker Integration:** RabbitMQ is managed within the application using Docker, similar to how the [Serilog Seq server](logging-implementation.md) is managed. This is done using the `RabbitMQDockerManager`, a utility class that handles the lifecycle of the RabbitMQ container. By leveraging the `Docker.DotNet` library, the application ensures that RabbitMQ is running before any message operations are attempted.
    *   **Configuration in Program.cs:** At the application startup, `RabbitMQDockerManager.ValidateDockerContainer()` is called to check if a RabbitMQ container is running. If not, the container is automatically started using the appropriate Docker commands. This approach ensures that RabbitMQ is always available and ready to handle messages, reducing the likelihood of downtime or message loss.

        ```csharp
        // Start the Docker container for RabbitMQ.
        await RabbitMQDockerManager.ValidateDockerContainer();
        ```


5.  **MessagePublisher Class**

    *   **Decoupling Responsibilities:** To maintain a clean and modular codebase, the responsibility of sending messages to RabbitMQ is separated from the repositories. The `MessagePublisher` class is introduced to handle all interactions with RabbitMQ, ensuring that the repositories do not need to be aware of the message broker's existence.

        ```csharp
        using RabbitMQ.Client;
        using System.Text;

        namespace FoodServiceAPI.Messaging
        {
            public class MessagePublisher
            {
                private readonly IModel _channel;

                public MessagePublisher(IModel channel)
                {
                    _channel = channel;
                }

                public void Publish(string routingKey, string message)
                {
                    var body = Encoding.UTF8.GetBytes(message);
                    _channel.BasicPublish(exchange: "",
                                          routingKey: routingKey,
                                          basicProperties: null,
                                          body: body);

                    Console.WriteLine($" [x] Sent '{message}' to queue '{routingKey}'");
                }
            }
        }
        ```
    * **Using MessagePublisher:** The `MessagePublisher` class is injected into services or repositories that need to send messages. This ensures that message transmission is handled consistently across the application.


6.  **Handling Errors and Retries**

    * **Dead-Letter Queues:** In cases where message processing fails, RabbitMQ supports dead-letter queues, which store failed messages for later analysis or retries. This feature is particularly useful for ensuring that no messages are lost and that errors can be handled gracefully.
    * **Retry Mechanism:** A retry mechanism can be implemented using RabbitMQ's built-in capabilities or by custom logic in the application. This ensures that transient errors do not cause messages to be permanently lost.



**Benefits of RabbitMQ in FoodServiceAPI**

* **Improved Coordination:** By using RabbitMQ, different parts of the system (e.g., kitchen staff, delivery personnel) can coordinate more effectively without direct dependencies, improving overall efficiency.
* **Real-Time Notifications:** Customers receive real-time updates on their orders, enhancing their experience and satisfaction.
* **Scalability:** RabbitMQ allows the application to scale horizontally, handling increased load without degradation in performance.
* **Reliability:** The Outbox pattern, along with RabbitMQ's robust message delivery features, ensures that messages are reliably processed even in the face of system failures.

