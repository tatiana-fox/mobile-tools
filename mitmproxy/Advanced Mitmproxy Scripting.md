# Advanced Mitmproxy Scripting

In addition to manipulating HTTP requests and responses, Mitmproxy's Python scripting capabilities allow you to perform more complex tasks.

## 1. Changing Response Body:

In some cases, you might want to alter the response body. Here's how to do it:

```python
def response(flow: http.HTTPFlow):
    if "json" in flow.response.headers.get("content-type", ""):
        data = json.loads(flow.response.text)
        data["new_field"] = "new_value"
        flow.response.text = json.dumps(data)
```

This script checks if the response content type is JSON and if so, it adds a new field to the JSON response.

## 2. Redirecting Requests:

You can redirect requests to a different server. This could be useful for testing your application against a mock server.

```python
def request(flow: http.HTTPFlow):
    if flow.request.pretty_host == "original.com":
        flow.request.host = "localhost"
        flow.request.port = 8081
```

This script will redirect all requests that were initially destined for 'original.com' to 'localhost' on port 8081.

## 3. Adding Delays:

You can add delays to responses, simulating a slow network or server. This can help you understand how your application behaves under these conditions.

```python
import time

def response(flow: http.HTTPFlow):
    time.sleep(5)  # delays the response by 5 seconds
```

Remember that the Python scripts should be passed to mitmproxy using the -s flag:

```shell
mitmproxy -s my_script.py
```

Mitmproxy's scripting capabilities can make it an incredibly powerful tool for debugging and testing applications. By combining these techniques, you can simulate a variety of network conditions and server responses.

## References:

[Mitmproxy Scripting](https://docs.mitmproxy.org/stable/overview-scripting/)
[Mitmproxy API](https://docs.mitmproxy.org/stable/api/overview/)

As always, use these tools responsibly. They can help you create a better experience for your users, but they should not be used to violate privacy or security.



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