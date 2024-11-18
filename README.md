# Chat-Application-based-on-WebSocket
WebSocket is a communication protocol that makes it possible to establish a two-way communication channel between a server and a client.

WebSocket works by first establishing a regular HTTP connection with the server and then upgrading it to a bidirectional websocket connection by sending an Upgrade header.

WebSocket is supported in most modern web browsers and for browsers that don’t support it, we have libraries that provide fallbacks to other techniques like comet and long-polling.

# Spring Boot WebSocket Chat Application

This project is a **real-time chat application** built with **Spring Boot** and **WebSockets**. It allows users to send and receive messages instantly without needing to refresh the page, providing a seamless and dynamic chat experience.

## Project Overview

The application utilizes **WebSocket** technology to enable full-duplex communication between the client and server, allowing users to send and receive messages in real-time. With the integration of **STOMP** and **SockJS**, this chat application ensures compatibility with various browsers and devices.

## Key Features
- **Real-time Communication**: Messages are instantly broadcast to all connected clients.
- **WebSocket Support**: Full-duplex communication over a persistent connection, providing fast message delivery.
- **STOMP Protocol**: Efficient message routing and delivery using the STOMP protocol over WebSocket.
- **Compatibility**: Uses **SockJS** to ensure that the application works even on browsers that don't support WebSockets natively.
- **Simple UI**: A clean and responsive frontend allowing users to type and send messages instantly.

## Technologies Used
- **Spring Boot**: For building the backend and handling WebSocket connections.
- **WebSockets**: For real-time, bidirectional communication between the client and the server.
- **STOMP**: A messaging protocol used over WebSockets to structure message exchanges between the client and server.
- **SockJS**: A JavaScript library that provides a WebSocket-like object for browsers that don't support WebSockets natively.
- **JavaScript**: For handling the client-side logic, such as connecting to WebSocket, sending messages, and displaying received messages.
- **HTML/CSS**: For creating a simple and user-friendly frontend.

## Project Structure

### 1. WebSocket Configuration
The WebSocket configuration class sets up the server-side behavior of WebSocket connections and message flow. It enables the WebSocket message broker and defines destinations for the clients to subscribe to and send messages to.

- **@EnableWebSocketMessageBroker**: Enables WebSocket messaging.
- **/topic**: Destination prefix for messages that clients subscribe to.
- **/app**: Destination prefix for messages that clients send to the server.
- **/chat**: The WebSocket endpoint where clients connect.

### 2. Message Controller
The message controller is responsible for handling incoming messages and broadcasting them to all connected clients.

- **SimpMessagingTemplate**: A Spring utility that is used to send messages to a specific destination, broadcasting the message to all clients subscribed to `/topic/messages`.

### 3. Frontend (HTML + JavaScript)
The frontend of the application is a simple HTML page where users can send and receive messages in real-time.

- **SockJS**: Ensures compatibility for WebSocket connections.
- **STOMP Client**: Allows clients to communicate with the server using the STOMP protocol.

### 4. Flow of Communication
1. **WebSocket Connection**: 
   - Clients connect to the `/chat` WebSocket endpoint, maintaining an open connection throughout their session.
   
2. **Message Flow**:
   - Clients send messages to the server via the `/app/send` endpoint.
   - The server broadcasts the message to all clients subscribed to `/topic/messages`.
   
3. **Client-Server Communication**:
   - Sending messages: The client sends messages using `stompClient.send("/app/send", {}, message)`.
   - Receiving messages: The client listens to the `/topic/messages` destination and displays messages instantly when they are received.

## How It Works

### 1. WebSocket Connection:
The application establishes a WebSocket connection between the client and the server at the `/chat` endpoint. The connection stays open for the duration of the session, allowing real-time, continuous communication.

### 2. Message Flow:
When a user types a message and presses "Send," the message is sent to the server via the `/app/send` endpoint. The server then broadcasts the message to all connected clients via the `/topic/messages` destination. All clients subscribed to this destination will receive the new message instantly.

### 3. Client-Server Communication:
- **Sending Messages**: 
  - The client sends messages using the following code: 
  ```javascript
  stompClient.send("/app/send", {}, message);
