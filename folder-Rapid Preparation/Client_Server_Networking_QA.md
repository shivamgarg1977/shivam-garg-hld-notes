# Client-Server Architecture & Networking Q&A

## 1. What is the Client-Server Architecture?
**Answer:** It is a distributed application architecture that partitions tasks between providers of a resource/service (servers) and service requesters (clients). Clients request resources, and servers process and serve those requests.

## 2. What are the layers of the TCP/IP model?
**Answer:**
1. **Application Layer:** Interacts with software applications (HTTP, FTP, SMTP).
2. **Transport Layer:** Ensures data arrives at the destination (TCP, UDP).
3. **Internet Layer:** Routes packets across networks (IP).
4. **Link Layer:** Handles physical transmission of data (Ethernet, Wi-Fi).

## 3. How does the TCP 3-Way Handshake work?
**Answer:** It establishes a connection before transmitting data:
1. **SYN:** Client sends a request to synchronize and initiate a connection.
2. **SYN-ACK:** Server acknowledges the request and sends its own synchronize request.
3. **ACK:** Client acknowledges the server's synchronize request. The connection is now established.

## 4. What is the difference between TCP and UDP?
**Answer:**
* **TCP (Transmission Control Protocol):** Connection-oriented, reliable, orders packets, slower. Used for HTTP, email, file transfers.
* **UDP (User Datagram Protocol):** Connectionless, unreliable, unordered, faster. Used for live streaming, gaming, VoIP.

## 5. What makes HTTP a "stateless" protocol?
**Answer:** Each HTTP request is completely independent. The server does not retain any information or state about previous requests from the same client. State is typically maintained using external mechanisms like Cookies or Sessions.

## 6. What is the difference between HTTP and HTTPS?
**Answer:**
HTTP transmits data in plain text, meaning anyone intercepting it can read the data.
HTTPS is secure and encrypted using TLS/SSL. It uses Port 443 (HTTP uses Port 80) and performs a TLS Handshake to exchange encryption keys and authenticate the server's digital certificate before transmitting data.

## 7. Explain common HTTP Status Codes.
**Answer:**
* **200 OK:** The request succeeded.
* **301 Moved Permanently:** Resource has been permanently moved to a new URL.
* **400 Bad Request:** Server could not understand the request due to invalid syntax.
* **401 Unauthorized:** Authentication is required and failed or has not been provided.
* **403 Forbidden:** Client does not have access rights to the content.
* **404 Not Found:** The server can not find the requested resource.
* **500 Internal Server Error:** The server encountered a situation it doesn't know how to handle.

## 8. What is the purpose of HTTP Headers? Give examples.
**Answer:** Headers pass additional information (metadata) with an HTTP request or response.
* **User-Agent:** Identifies the client software/browser.
* **Content-Type:** Indicates the media type of the resource (e.g., `text/html`, `application/json`).
* **Cache-Control:** Specifies directives for caching mechanisms.
* **Authorization:** Contains credentials to authenticate a user with a server.
