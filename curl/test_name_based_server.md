# How to test name based servers locally?

## The problem

You run a web application via **nginx** and you dispatch the requests based on the server name.

And maybe the server name header only gets set via an URL, which is currently or permanent not available in your dev setup.

## The solution

```
curl -- header "Host: example.com" http://localhost
```

## Further information

Blog post by the maintainer of curl:

https://daniel.haxx.se/blog/2018/04/05/curl-another-host/
