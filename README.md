# SocksLib

**SocksLib** is a Java library for **SOCKS5** protocol.

#### References
 
* [SOCKS Protocol Version 5](http://www.ietf.org/rfc/rfc1928.txt)
* [Username/Password Authentication for SOCKS V5](http://www.ietf.org/rfc/rfc1929.txt)

## Features

### ⚠ This fork includes the following changes ⚠

- Updated dependencies
- Removed MongoDB related features

Obtain this library via [Github](https://github.com/HyperCDN/sockslib/packages/) or [Jitpack](https://jitpack.io/#HyperCDN/sockslib) using Maven or Gradle

### Client

* TCP proxy
* UDP proxy
* Bind
* Anonymous authentication
* USERNAME/PASSWORD authentication
* Proxy chain

### Server

* TCP proxy
* UDP proxy
* Bind
* Anonymous authentication
* USERNAME/PASSWORD authentication
* Proxy chain
* Black or white IP lists for clients

## Quick start

#### Environment

* JDK 8+

### SOCKS5 Client

#### CONNECT

```java
    SocksProxy proxy = new Socks5(new InetSocketAddress("localhost",1080));
    Socket socket = new SocksSocket(proxy, new InetSocketAddress("whois.internic.net",43));
```

Connect SOCKS5 server using SSL connection

```java
    SSLConfigurationBuilder builder = SSLConfigurationBuilder.newBuilder();
    builder.setTrustKeyStorePath("client-trust-keystore.jks");
    builder.setTrustKeyStorePassword("123456");
    SocksProxy proxy = new SSLSocks5(new InetSocketAddress("localhost", 1081), builder.build());
    Socket socket = new SocksSocket(proxy, new InetSocketAddress("whois.internic.net",43));
```

#### BIND

```java
    SocksServerSocket serverSocket = new SocksServerSocket(proxy, inetAddress,8080);
    InetAddress bindAddress = serverSocket.getBindAddress();
    int bindPort  = serverSocket.getBindPort();
    Socket socket = serverSocket.accept();
```

#### UDP ASSOCIATE

```java
     DatagramSocket socket = new Socks5DatagramSocket(proxy);
```

### SOCKS5 Server

```java
     SocksProxyServer proxyServer = SocksServerBuilder.buildAnonymousSocks5Server(); 
     proxyServer.start();// Creat a SOCKS5 server bind at port 1080
```

SSL socks server

```java
    SSLConfigurationBuilder builder = SSLConfigurationBuilder.newBuilder();
    builder.setKeyStorePath("server-keystore.jks");
    builder.setKeyStorePassword("123456");
    builder.setClientAuth(false);
    socksProxyServer = SocksServerBuilder.buildAnonymousSSLSocks5Server(1081, builder.build());
    socksProxyServer.start();
```
