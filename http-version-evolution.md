---
title: HTTP version evolution
published: true
description: 
tags: HTTP, network 
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/1deshry2rg4lnxo6dnts.jpg)

The **HTTP** protocol is the communication language between the browser and the server, the latest version has reached **HTTP 3.0**.

I have read some articles and made some records of the evolution of the **HTTP** version. here I will share some key points for you



### First version HTTP/0.9

First verssion **HTTP** mainly used for academic communication. used to transfer **HTML** hypertext content between networks, using a request-response model.  a request is sent from the client and the server returns data. 

In general the demand at that time was very simple, it was used to transmit small **HTML** files. 

Has three characteristics:

* There is only one request line. and there is no **HTTP** request header and request body

* The server did not return header information

* The content of the returned file is transmitted as a stream of **ASCII** characters



### HTTP/1.0

Supporting multiple types of file downloads is a core requirement of **HTTP/1.0**. including **JavaScript**, **CSS**, **pictures**, **audio**, **video** etc.

**HTTP/1.0** negotiates and communicates through request headers and response headers. requesting file types and returning file types. E.g

``` html
// request
accept: text/html
accept-encoding: gzip, deflate, br
accept-Charset: ISO-8859-1,utf-8
accept-language: zh-CN,zh

// response
content-encoding: br
content-type: text/html; charset=UTF-8
```



### HTTP/1.1

**HTTP/1.1** has made a lot of updates on the basis of **HTTP/1.0** including

* Improve the persistent connection. multiple **HTTP** requests can be transmitted on a **TCP** connection. as long as the browser or server does not explicitly disconnect, the **TCP** connection will be maintained.

* Immature **HTTP** pipeline to solve the problem of queue blocking by pipeline technology.

* Provide virtual host support, the **Host field**  is added to the request header to indicate the current domain name address, so that the server can do different processing according to different Host values.

* Provides perfect support for dynamically generated content, introducing **chunk transfer** mechanism. the server will divide the data into several data blocks of any size, each data block will be attached with the length of the last data block, and finally use a zero-length block as a sign of sending data

* Client **cookies** security mechanism



Continue to share tomorrow， Hope it can help you  :)
