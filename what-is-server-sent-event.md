---
title: What is Server Sent Event
published: true
description: 
tags: Javascript
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/edpotichzeo6qtfpvoal.jpg)

The Server Sent Events specification describes a built-in class `EventSource`, that keeps connection with the server and allows to receive events from it. similar to `WebSocket` it’s simpler. In many applications, the power of `WebSocket` is a little bit too much.

What difference:

* One-directional: only server sends data

*  Only text

* Regular HTTP


### Getting messages

1. To start receiving messages, we just need to create `new EventSource(url)`.
2. The browser will connect to `url` and keep the connection open, waiting for events.
3. The server should respond with status 200 and the header `Content-Type: text/event-stream`

```javascript
let eventSource = new EventSource("/events/channel");
eventSource.onmessage = function(event) {
  console.log("New message", event.data);
};
```

### Reconnection

Upon creation, `new EventSource` connects to the server, and if the connection is broken – reconnects. that’s very convenient, as we don’t have to care about it.



### Close

```javascript
let eventSource = new EventSource(...);
eventSource.close();
```



### Event types

By default `EventSource` object generates three events:

- `message` – a message received, available as `event.data`.
- `open` – the connection is open.
- `error` – the connection could not be established, e.g. the server returned HTTP 500 status.



Hope it can help you :)


