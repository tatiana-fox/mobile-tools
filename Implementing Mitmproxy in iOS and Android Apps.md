# Implementing Mitmproxy in iOS and Android Apps

Mitmproxy is an open-source proxy tool used to intercept, inspect, modify and replay HTTP, HTTPS, WebSockets, and HTTP/2 traffic. Here is how you can implement mitmproxy in iOS and Android apps.

## iOS:

### Step 1: Install Mitmproxy

First, you need to install mitmproxy. It can be installed on macOS using Homebrew:

```shell
brew install mitmproxy
```

### Step 2: Setup iPhone

Configure your iPhone’s Wi-Fi settings. Go to your current Wi-Fi network’s settings and set the HTTP Proxy setting to ‘Manual’. Enter your computer’s IP address in the ‘Server’ field and ‘8080’ (default) in the ‘Port’ field.

### Step 3: Install Mitmproxy Certificate

Visit mitm.it from your iPhone. You should see an option to install the mitmproxy certificate. Go ahead and install it.

Then, go to Settings > General > About > Certificate Trust Settings. Under “Enable full trust for root certificates,” turn on the switch for the new certificate.

### Step 4: Run Mitmproxy

Back to your computer, run:

```shell
mitmproxy
```

Then, start your application on your iPhone. You will see the network traffic from your device in your computer terminal.

## Android:

### Step 1: Install Mitmproxy

You can use the same installation command as for iOS:

```shell
brew install mitmproxy
```

### Step 2: Setup Android Device

Connect your Android device and your computer to the same Wi-Fi network. Modify your Wi-Fi network settings and set up the proxy. The proxy hostname is your computer’s IP address, and the proxy port is ‘8080’ (default).

### Step 3: Install Mitmproxy Certificate

On your Android device, visit mitm.it and install the mitmproxy certificate.

For Android Nougat and above, you have to create a new Network Security Configuration file where you declare that user-installed CAs are trusted.

```xml
<network-security-config> 
  <base-config> 
    <trust-anchors> 
      <certificates src="system" /> 
      <certificates src="user" /> 
    </trust-anchors> 
  </base-config> 
</network-security-config>
```

Reference the Network Security Config file in your AndroidManifest.xml

```xml
<?xml version=“1.0" encoding=“utf-8”?>
<manifest ... >
    <application android:networkSecurityConfig=“@xml/network_security_config”
                    ... >
        ...
    </application>
</manifest>
```

### Step 4: Run Mitmproxy

Back on your computer, run:

```shell
mitmproxy
```

Then, start your application on your Android device. You will see the network traffic from your device in your computer terminal.

This setup enables the interception of traffic from your iOS and Android apps. Happy debugging!

Please remember, certificate handling can be different between devices and OS versions, so always refer to the official mitmproxy documentation for the most up-to-date and detailed instructions.

## References:
* [Mitmproxy documentation](https://docs.mitmproxy.org/stable/)
* [Mitmproxy on iOS](https://docs.mitmproxy.org/stable/howto-iphone/)
* [Mitmproxy on Android](https://docs.mitmproxy.org/stable/howto-android/)
