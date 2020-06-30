---
title: HTTP version evolution 2 
published: true
description: 
tags: HTTP
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/3rmlzrhjnewq46j5hdhx.jpg)

I have record article about **HTTP** beginning at [HTTP version evolution](https://dev.to/ihavecoke/http-version-evolution-2cef). this article i will share my note with **HTTP** evolution 2

### What are the problems with HTTP/1.1

##### HTTP 1 features 

* Added persistent connections 
* The browser maintains up to 6 TCP persistent connections simultaneously for each domain name
* Using CDN to realize the domain name fragmentation mechanism

##### HTTP problems

The problems is utilization of bandwidth is not ideal

> Bandwidth refers to the maximum number of bytes that can be sent or received per second. 
>
> the maximum number of bytes that can be sent per second is called **upstream bandwidth**
>
> the maximum number of bytes that can be received per second is  **downstream bandwidth**

The reason why **HTTP/1.1** is not ideal for bandwidth utilization is because it is difficult for **HTTP/1.1** to use up bandwidth for the following three reasons

* **TCP ** slow start
* Simultaneously open multiple **TCP** connections, then these connections will compete for fixed bandwidth
* The problem of **HTTP/1.1** queue blocking.

### HTTP 2.0 

To solve the above problem the idea of  **HTTP/2** is that a domain name uses only one long **TCP** connection to transmit data, and realizes parallel requests for resources,it can send requests to the server at any time without waiting for the completion of other requests.

#### Multiplexing implementation

##### The introduction of the binary framing layer realizes the multiplexing technology of HTTP

* First the browser prepares the request data, including the request line, request header, and other information. If it is the **POST **method then there must be a request body.
* After the data is processed by the binary frame layer, it will be converted into frames with request ID numbers, and these frames will be sent to the server through the protocol stack. 
  After receiving all the frames, the server will merge all the frames with the same ID into a complete request message.
* The server then processes the request and sends the processed response line, response header, and response body to the binary framing layer, respectively.
* Similarly the binary framing layer converts these response data into frames with request ID numbers and sends them to the browser through the protocol stack.
* After receiving the response frame, the browser will submit the frame data to the corresponding request according to the ID number.

#### Other features

* You can set the priority of the request, when sending the request mark the priority of the request
* Server push you can directly push the data to the browser in advance
* Header compression, which compresses the request header and response header



Hope it can help you :)


