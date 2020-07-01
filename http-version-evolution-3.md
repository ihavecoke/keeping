---
title: HTTP version evolution 3
published: false
description: 
tags: HTTP
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/crudsnlj7dkf4e85wy2j.jpg)


I have record article about HTTP/1 和 HTTP/2 at [HTTP version evolution](https://dev.to/ihavecoke/http-version-evolution-2cef) [HTTP version evolution 2](https://dev.to/ihavecoke/http-version-evolution-2-34kh) this article i will share my note with **HTTP** evolution 3

### TCP header block

Although **HTTP/2** solves the queue-blocking problem at the application level, the queue-blocking problem caused by the loss of a single packet in **TCP** is called queue-blocking over **TCP**. 

Test data shows that **HTTP/1.1** transport efficiency is better than **HTTP/2** when the system reaches a 2% packet loss rate.



#### The delay in establishing a TCP connection

Network delay is also called **Round Trip Time**. We refer to the total round-trip time between sending a packet from the browser to the server and returning the packet from the server to the browser as **RTT**, which is an important indicator of network performance.

* When establishing a **TCP** connection, three handshakes with the server are required to confirm the connection, which means that 1.5 **RTT** is consumed before data can be transmitted.
* **TLS** connections are made. there are two versions of **TLS** -- **TLS1.2** and **TLS1.3**

We need to spend 3-4 **RTTS** before transmitting the data



#### TCP protocol ossification

Include router, firewall, NAT, switch and so on. they often rely on little-updated software that USES a lot of **TCP** features that are set up and rarely updated.



#### QUIC protocol

Based on **UDP** it realizes the functions of multiple data streams and transmission reliability similar to **TCP**. We call this set of functions **QUIC protocol**

* Realize functions like **TCP** flow control and transmission reliability
* Integrated **TLS** encryption function
* Implemented the multiplexing function in  **HTTP/2 **
* Implemented a quick handshake function



#### HTTP/3

* Neither the server nor the browser provides complete support for **HTTP/3**
* There are also very big problems in deploying **HTTP/3** because the system kernel's optimization of **UDP** is far from **TCP** optimization, this is also an important reason that hinders **QUIC**
* The problem of the rigidity of the middle equipment. the optimization of **UDP** by these devices is much lower than **TCP**. according to statistics, when using **QUIC** protocol there is about 3% to 7% packet loss rate.


Hope it can help you :)
