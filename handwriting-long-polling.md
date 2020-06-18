---
title: Handwriting long polling
published: true
description: how to write long polling connect in javascript
tags: JavaScript, Tricks
---

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/vaee4954xeoavlus09p3.jpg)

Generally speaking we should use long connect in some real time communication scenes like: chat, web game etc.

`WebScoket` is useful tech to implement real time communication also `Server Side Events` is.

How to implement **long polling** manual? let's begin


### The flow:

1. A request is sent to the server.
2. The server doesn’t close the connection until it has a message to send.
3. When a message appears – the server responds to the request with it.
4. The browser makes a new request immediately.

### The code:

```javascript
async function subscribe() {
  let response = await fetch("/subscribe");
  if (response.status == 502) {
    await subscribe();
  } else if (response.status != 200) {
    notify(response.statusText);
    await new Promise(resolve => setTimeout(resolve, 1000));
    await subscribe();
  } else {
    let message = await response.text();
    notify(message);
    await subscribe();
  }
}
subscribe();
```

`subscribe` will await request response

If response **502** maybe network error will try call `subscribe` again. 

If response not ok(response status not equal 200) will notify error message and after one second try call `subscribe` again. 

Else if response ok  notify response body and immediately call `subscribe` again

Simply say `subscribe` function makes a fetch, then waits for the response, handles it and calls itself again.



Hope it can help you :)
