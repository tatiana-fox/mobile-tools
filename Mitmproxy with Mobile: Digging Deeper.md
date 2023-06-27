# Mitmproxy with Mobile: Digging Deeper

While we have covered the basic setup of Mitmproxy with iOS and Android, there are more specific applications and advanced use cases you might encounter while testing or debugging mobile apps.

## 1. SSL Pinning:

Some mobile apps use a security feature known as SSL pinning, which can cause issues when trying to intercept traffic with Mitmproxy. The app may not trust the Mitmproxy certificate, even after it has been installed on the device. In this case, you'll need to remove or bypass the pinning in the app code itself.

For iOS apps, this could be done using tools like [objection](https://github.com/sensepost/objection) or [SSL Kill Switch](https://github.com/nabla-c0d3/ssl-kill-switch2).

For Android, you can use [Frida](https://www.frida.re/) or [Objection](https://github.com/sensepost/objection) as well.

Remember to only use these methods for ethical purposes such as testing your own apps.

## 2. Simulating Network Conditions:

Mitmproxy can be used to simulate different network conditions, which is useful for understanding how your mobile app performs under various scenarios. For example, you could simulate a slow network connection using the following script:

```python
import time

def request(flow: http.HTTPFlow):
    time.sleep(2)  # adds a 2 second delay to every request
```

## 3. Automated Testing:

You can use Mitmproxy in conjunction with automated testing tools. For instance, you could create a script that modifies certain responses and then run your app's test suite to see how it behaves.

## 4. Exploring App Behavior:

Mitmproxy can also be used to explore how an app behaves, which can be useful for performance optimization. By examining the requests an app makes, you can gain insights into its operations, allowing you to identify potential bottlenecks or unnecessary requests.

## 5. App-Specific Scripts:

Every app is different, and you may find that you need to write Mitmproxy scripts tailored specifically to your app's behavior. These scripts can leverage any part of the Mitmproxy API, allowing you to craft custom solutions for your needs.

Mitmproxy is a versatile tool that can be an invaluable part of a mobile app developer's toolkit. Always ensure that you are using it responsibly and ethically.

## References:

* [Mitmproxy API](https://docs.mitmproxy.org/stable/addons-overview/)
* [Objection GitHub](https://github.com/sensepost/objection)
* [Frida](https://www.frida.re/)
* [SSL Kill Switch](https://github.com/nabla-c0d3/ssl-kill-switch2)