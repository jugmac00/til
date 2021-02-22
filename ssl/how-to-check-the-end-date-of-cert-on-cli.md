# How to the end date of an SSL/TLS certificate?

For a couple of years now, I use the fantastic (and free*) service by [Let's Encrypt](https://letsencrypt.org/) in order to generate SSL/TLS certificates.

One of the main differences to paid certs is that the ones of **Let's Encrypt** are only valid 90 days.

This sounds bad at first, but actually this is a good thing from a security perspective,
and anyway, you do not create / renew certs manually, but one of the many clients do this for you automatically.

Today I got a notification from the `Let's Encrypt Expiry Bot` that one of my domains' certificate is about to expire.

## How to check the end date?

While for web services you can check the end date by clicking on the **lock** symbol in the browser,
how do you this when you just have access to the certificate file, e.g. `cert.pem`?

### Use the client tooling

I use [Certbot](https://certbot.eff.org/) to manage my certifications, so all I need to do is entering...

```
# certbot certificates

  Certificate Name: xxx.example.com
    Domains: abc.example.com def.example.com xxx.example.com
    Expiry Date: 2021-04-04 12:49:35+00:00 (VALID: 41 days)
    Certificate Path: /etc/letsencrypt/live/xxx.example.com/fullchain.pem
    Private Key Path: /etc/letsencrypt/xxx.example.com/privkey.pem
```

All good!

### Use openssl

You can also use the **swiss knife** of ssl handling on Linux...

```
$ openssl x509 -enddate -noout -in cert/xxx.example.com/cert.pem 

notAfter=Apr  4 12:49:35 2021 GMT
```

All good!

So, it looks like this was a false alarm!


*) The service is free for all, but the organization has to pay its bills, the infrastructure cost and its employees.

I donated and you should probably too if you can afford it: [Official donation page](https://letsencrypt.org/donate/)
