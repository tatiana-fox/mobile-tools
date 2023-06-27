# Making the Most of Mitmproxy's Event Hooks

Mitmproxy's Python scripting API provides a number of event hooks that you can use to take action at different stages of a request or response. Here are a few of them:

## 1. request:

This hook is triggered when a request is received. It's useful for modifying the request before it's sent to the server.

```python
def request(flow: http.HTTPFlow):
    flow.request.headers["x-custom-header"] = "custom_value"
```

## 2. response:

This is triggered when a response is received. It's where you can modify the server's response before it's sent back to the client.

```python
def response(flow: http.HTTPFlow):
    flow.response.headers["x-custom-header"] = "custom_value"
```

## 3. error:

The error hook is triggered when there's an error in handling a request or response. It's useful for logging or handling errors.

```python
def error(flow: http.HTTPFlow):
    ctx.log.error(f"Error: {flow.error}")
```

## 4. websocket_handshake:

This hook is triggered when a WebSocket handshake is initiated. You can modify the handshake here.

```python
def websocket_handshake(flow: http.HTTPFlow):
    flow.request.headers["origin"] = "http://example.com"
```

## 5. websocket_message:

This is triggered for every WebSocket message sent or received.

```python
def websocket_message(flow: websocket.WebSocketFlow):
    message = flow.messages[-1]
    message.content = message.content.replace(b"old", b"new")
```

You can combine these hooks in a single script, and they'll be triggered as appropriate when you run Mitmproxy.

```python
def request(flow: http.HTTPFlow):
    # ...

def response(flow: http.HTTPFlow):
    # ...

def error(flow: http.HTTPFlow):
    # ...

def websocket_handshake(flow: http.HTTPFlow):
    # ...

def websocket_message(flow: websocket.WebSocketFlow):
    # ...
```

You can find the full list of event hooks in the [Mitmproxy documentation](https://docs.mitmproxy.org/stable/addons-events/).

## References:
[Mitmproxy Event Hooks](https://docs.mitmproxy.org/stable/addons-events/)