# Module 8: Software Architectures
## Tutorial Advanced Programming 2023/2024 Genap

* Nama  : Tengku Laras Malahayati
* NPM   : 2206081641
* Kelas : A

## Reflection
### What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

- **Unary RPC Methods**: The client sends a single request to the server then wait for it to send back a response. Inside the request, there are some procedures that are needed to be executed by the server. As a result, the server sends back the executing result as a response.  This method is commonly used as a substitute for REST API since it performs a simple query-response type of communication between client and server.
- **Server Streaming RPC Methods**: The client sends a single request to the server then receives multiple continous streams from the server. This happens because the server needs to send back a large amount of the data by chunking it into a number of streams of smaller amount data. It can also be a result of asynchronous processing if the method allows the server to send partial results. As a result, it allows the client to receive realtime stream of data from the server.
- **Bi-directional Streaming RPC Methods**: Both the client and server send a stream of messages to each other using read-write procedures. The streams are not strictly follow a request-response flow so each stream is independent from one to another. This allows both the client and server to read and write in the same time. This method is usually used when there needs to be a realtime and interactive communication between the client and server, such as multiplayer gaming and collaborative editing.

### What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

There are some security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption.
- **Authentication**: This ensures security by making sure that clients who have access are who they claim to be. It can be achieved by using authentication mechanisms such as API keys or JWT tokens. 
- **Authorization**: This ensures security by making sure that each authenticated client has their own rights and restrictions to prevent unauthorized access to sensitive data or operations. It can be implemented by enforcing a fine-grained access control to data or information.
- **Data Encryption**: This ensures security by protecting data or sensitive information from unauthorized access or operations. One of the ways to achieve security in data is by using encryption algorithm such as RSA for securing data. 

### What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

Handling bidirectional streaming in Rust using gRPC can pose to several challenges. These include managing error handling for issues that arise during streaming, ensuring proper synchronization as clients send requests and receive responses from servers, and maintaining concurrency and scalability to support a large number of simultaneous connections and streams. Additionally, latency can impact the performance and responsiveness of the system. Navigating these challenges is crucial for maintaining secure, efficient communication between clients and servers, and requires careful consideration of the mentioned issues.

### What are the advantages and disadvantages of using the `tokio_stream::wrappers::ReceiverStream` for streaming responses in Rust gRPC services?

Using `tokio_stream::wrappers::ReceiverStream` converts `tokio::sync::mpsc::Receiver` into a `Stream` that enable the server to send a continuous stream of messages to the client. It supports integrate asynchronous communication flow by working with streams in Rust. However, this approach can introduce complexities, particularly for those who are less familiar with asynchronous programming in Rust. Additionally, it may necessitate enhanced error handling and synchronization measures to ensure that the stream is appropriately terminated and cleaned up as needed.

### In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

The Rust gRPC code could be structured to facilitate code reuse and modularity by following best practices and design patterns to promote maintainability and extensibility over time. It is achievable by applying knowledge that has been taught in class, such as SOLID Principle, concern separation, and using appropriate abstractions in our code. Another ways to achieve it would be applying the right ways to avoid code duplication and applying libraries (in import statements).

### In the `MyPaymentService` implementation, what additional steps might be necessary to handle more complex payment processing logic?

To handle more complex payment processing logic, we can add authentication process (to ensure that only authenticated users are able to make payment) or even modify the `process_payment` method to be a server-streaming method to handle response sending to clients for a more efficient data sending process.

### What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

Implementing gRPC as a communication protocol enhances interoperability across various technologies and platforms. This is achieved by using Protocol Buffers as its interface definition language which makes gRPC language-agnostic. As a result, services written in different programming languages and operating on various platforms can communicate as though they are executing natively within each environment, despite actually running on distinct platforms and languages. This setup significantly improves cross-language and cross-platform communication.

### What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

Some of the advantages of using HTTP/2 are:
- HTTP/2 allows sending and receiving multiple requests and responses over a single connection
- HTTP/2 reduces network overhead and improves performance by using header compression, binary protocol (comparing to HTTP/1.1's text-based protocol), and server push

However, it comes with disadvantages in terms of complexity (hard to implement), compability (not all servers and clients support HTTP/2), and resource consumption (because it can consume more server resources).

### How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

REST API, unlike gRPC, does not support real-time communication. In a REST-based setup, the client sends a request to the server, waits for a response, and is unable to send or receive additional data or requests until the initial task is complete. This model is less effective for real-time communication because it is not well-suited for scenarios where continuous updates from the server to the client are required. This limitation is evident in contrast to the responsiveness of real-time, bidirectional streaming found in applications like Google Docs, where multiple users can simultaneously edit the same document.

### What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

gRPC using Protocol Buffers offer more compability and supports by improving cross-language and cross-platform communication. By implementing a defined schema, gRPC ensures that messages retain their structure and are not lost when transferred between different applications and services. This contrasts with REST APIs, which typically use XML or JSON payloads that may not consistently maintain structural integrity across different platforms. Moreover, it focuses only on performing serialization and deserialization by removing responsibilities that are supposed to be done by dara formats, so that it ensures that the data is transmitted ASAP and in the most compact way which is VERY VALUABLE when working with microservices (minimizing data transimission time and size) (karena yg penting datanya ditransfer cepet dan TETAP TERJAGA).