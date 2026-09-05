# Q&A: Real-Time Networking (Polling, WebSockets, SSE)

## 1. What is the difference between Short Polling and Long Polling?
**Answer:** 
*   **Short Polling:** The client sends an HTTP request to the server at fixed, regular intervals (e.g., every 5 seconds) to check for new data. If the server has no data, it immediately returns an empty response. This is highly inefficient and creates significant network overhead.
*   **Long Polling:** The client sends an HTTP request, but if the server has no new data, it *holds the connection open* until data is available or a timeout occurs. Once the server responds, the client immediately sends a new request. This is more efficient as it reduces empty responses.

## 2. Why might an application choose Long Polling over WebSockets?
**Answer:** While WebSockets are more efficient for real-time bidirectional communication, Long Polling is built on standard HTTP. It is easier to implement in legacy environments, works seamlessly with existing HTTP load balancers and proxies, and doesn't require maintaining a stateful, persistent TCP connection in the same way WebSockets do. 

## 3. What are WebSockets?
**Answer:** WebSockets provide a persistent, full-duplex (two-way) communication channel over a single TCP connection. Both the client and the server can send messages to each other at any time independently, without the overhead of HTTP headers for every message.

## 4. How does a WebSocket connection begin?
**Answer:** It begins with a standard HTTP GET request from the client to the server. The client includes specific headers (`Connection: Upgrade` and `Upgrade: websocket`). If the server supports WebSockets, it responds with an `HTTP 101 Switching Protocols` status code, and the connection is successfully "upgraded" from HTTP to a WebSocket connection.

## 5. What are Server-Sent Events (SSE)?
**Answer:** SSE is a mechanism that allows a server to asynchronously push data to the client once an initial client connection has been made. It uses standard HTTP and holds the connection open, but unlike WebSockets, it is strictly **uni-directional** (data flows from Server to Client only). 

## 6. Compare WebSockets and SSE. When would you use one over the other?
**Answer:**
*   **WebSockets:** Bi-directional, lower overhead after handshake, uses a custom protocol (WS/WSS). Best for applications requiring heavy two-way communication like multiplayer browser games, collaborative drawing tools, or fast-paced chat applications.
*   **SSE:** Uni-directional (Server -> Client), uses standard HTTP, has built-in auto-reconnection and event IDs. Best for applications that only need to receive live updates, such as live sports scoreboards, stock tickers, or social media news feeds.

## 7. What is the overhead difference between WebSockets and standard HTTP requests?
**Answer:** Standard HTTP requests include a significant amount of overhead in the form of headers (cookies, user-agent, authorization, etc.) sent with *every* request and response. WebSockets only incur this overhead during the initial HTTP handshake. Subsequent WebSocket data frames have only a few bytes of overhead, making them vastly more efficient for sending many small messages rapidly.
