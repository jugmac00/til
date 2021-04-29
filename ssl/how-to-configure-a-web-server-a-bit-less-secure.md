# How to configure a web server a bit less secure?

This question sounds odd.
Why would you want a less secure web server?

Well, maybe you have to support older clients.

e.g. IE 11 on Windows 8.1 or Java 7 (cough) cannot connect to a web server, which only uses modern and secure ciphers.

From a Java application, which cannot be updated, but has to work, I got the following exception:

```
Exception in thread "main" javax.net.ssl.SSLHandshakeException: Received fatal alert: handshake_failure
	at sun.security.ssl.Alerts.getSSLException(Alerts.java:192)
	at sun.security.ssl.Alerts.getSSLException(Alerts.java:154)
	at sun.security.ssl.SSLSocketImpl.recvAlert(SSLSocketImpl.java:1979)
	at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:1086)
	at sun.security.ssl.SSLSocketImpl.performInitialHandshake(SSLSocketImpl.java:1332)
	at sun.security.ssl.SSLSocketImpl.startHandshake(SSLSocketImpl.java:1359)
	at sun.security.ssl.SSLSocketImpl.startHandshake(SSLSocketImpl.java:1343)
	at sun.net.www.protocol.https.HttpsClient.afterConnect(HttpsClient.java:559)
	at sun.net.www.protocol.https.AbstractDelegateHttpsURLConnection.connect(AbstractDelegateHttpsURLConnection.java:185)
	at sun.net.www.protocol.http.HttpURLConnection.getInputStream(HttpURLConnection.java:1301)
	at sun.net.www.protocol.https.HttpsURLConnectionImpl.getInputStream(HttpsURLConnectionImpl.java:254)
	at com.apisgroup.Main.main(Main.java:21)
```

Note to myself - writing clear and helpful exceptions messages could work wonder.

So, what was going on?
Obviously, there was a problem with the handshake. But why?

As this was a regression, I compared the old server setup and the setup after an OS and web server update.

[nginx](https://www.nginx.com/) came with a new default configuration, and with more secure ciphers.

https://www.ssllabs.com/ssltest/ showed an A-rating, all good!
Except the Java application could no longer communicate with the server.

# configuring a secure server is easy

So, configuring a secure server is easy, well, when you follow the correct resources and when you trust that those give reliable recommendations.

Configuring a server less secure is harder... which cipher may I allow although it is less (how much less?) secure?

I am by no means a security specialist, but here are some fine resources:

- https://www.ssllabs.com/ssltest/ -> test your site's certificate and configuration
- https://ciphersuite.info/ -> is a given cipher secure?
- https://www.openssl.org/docs/manmaster/man1/openssl-ciphers.html#CIPHER-LIST-FORMAT -> format of openssl's cipher notation
- `openssl ciphers` -> list available ciphers
- https://hynek.me/articles/hardening-your-web-servers-ssl-ciphers/ -> constantly updated guide how to configure a web server securely
- https://www.feistyduck.com/bulletproof-tls-newsletter/ -> latest security news in your inbox
- https://www.feistyduck.com/books/bulletproof-ssl-and-tls/ -> highly recommended read when you want to dive into this topic
- https://ssl-config.mozilla.org/ -> ssl configuration generator; modern + intermediate + old

After working through some of them, it still did not work.
- Mozilla's **intermediate** configuration still prevented access (for IE 11 on Windows Server 2012)
- my manual setup did not work - the dhe cipher did not show up at SSLLabs...

Note to myself: When you allow diffie hellmann exchange, please make sure to include the dhparams file :-/ ... or scratch your head for a while like I did.

The final solution emerged from a debugging session with my friendly hoster ([FlyingCircus](https://flyingcircus.io/)), looking here and there (hey gitlab!), doing this and that... and finally I got an A rating from SSLLabs, and still allow access for IE 11 and Java 7.

My next step: Dig into https://www.feistyduck.com/books/bulletproof-ssl-and-tls/ - 470 pages, here I come!
