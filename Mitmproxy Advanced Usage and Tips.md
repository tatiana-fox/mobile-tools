# Mitmproxy Advanced Usage and Tips

Once you’ve set up Mitmproxy on iOS and Android, there’s a world of opportunities to dig into your application’s network behavior. Here are some of the things you can do with Mitmproxy.

## 1. Interception and Modification:

Mitmproxy allows you to intercept and view all HTTP(s) requests/responses between the client and the server. But that’s not all! You can modify these requests or responses on the fly before they reach their destination.

For example, if you want to modify the request before it reaches the server, use the following command:

```python
def request(flow: http.HTTPFlow) -> None:
    # pretty_url takes the “Host” header of the request into account, which 
    # is useful in transparent mode where we could intercept any hostname.
    if flow.request.pretty_url.endswith(“/path/“):
        flow.request.path = “/modified/path/”
```

## 2. Replaying Traffic:

You can save request/response pairs and replay them later. This is very useful for debugging your app’s behavior in response to server-side changes.

Use the following command to save flows to a file:

```shell
mitmdump -w flowsfile
```

And this command to replay them:

```shell
mitmdump -c flowsfile
```

## 3. Scripting with Python:

You can use Python scripts to manipulate the traffic that passes through Mitmproxy. For instance, you can inject headers or manipulate responses.

Here’s an example Python script that adds a custom header:

```python
from mitmproxy import ctx

class AddHeader:
    def response(self, flow):
        flow.response.headers[“new-header”] = “custom_value”

addons = [
    AddHeader()
]
```

Then, you can run mitmproxy with the script:

```shell
mitmproxy -s add_header.py
```

## 4. Using Mitmweb:

Mitmweb is the web-based companion to Mitmproxy, offering a web-based user interface to inspect and manipulate traffic. To use it, just run:

```shell
mitmweb
```

Mitmweb allows you to filter, intercept, and modify requests using a graphical interface, which can be a more intuitive way of working with the tool.

Mitmproxy is a powerful tool that offers many other features. The above are just a few examples of what it can do. For a full list of capabilities, always refer to the [official Mitmproxy documentation](https://docs.mitmproxy.org/stable/).
