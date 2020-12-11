# How to access Zope via WebDav?

**WebDav** is a protocol, based on top of HTTP, that allows clients remote content authoring, such as creating, editing and deleting content.

The protocol itself is pretty old, dating back to the late 90ies.

While not really popular, even modern systems like `NextCloud`, `OwnCloud` and also the widely-used NAS systems by **Synology** do support this standard - and also Zope!

## How to activate WebDav support in Zope?

The WebDav support in Zope habd been temporarily removed, as Zope switched from the legacy ZServer to the standard WSGI approach, and WebDav was coupled to the ZServer, for no obvious reasons.

After WebDav support was restored, a couple of users tried to use it, but failed to configure WebDav support in Zope properly.

As Zope now uses the WSGI approach, WebDav support has to be configured both in Zope and for the WSGI server.

For example, when you use the `waitress` WSGI server and want to enable WebDav support for port 9090:

In the waitress configuration, you have to set..
```
[server:main]
use = egg:waitress#main
listen = 127.0.0.1:9090 127.0.0.1:8080
```

In the Zope configuration, you have to set...
```
webdav-source-port 9090
```

## How to access Zope via WebDav?

I never used WebDav, and so I looked around for a client.

Ubuntu offers `Cadaver` in its repositories.

```
sudo apt install cadaver
```

```
❯ cadaver localhost:9090
Authentication required for Zope on server `localhost':
Username: admin
Password: 
dav:/> ls
Listing collection `/': succeeded.
        acl_users                              0  Okt  9 13:44
        hello.txt                              6  Okt  9 13:44
        index_html                           434  Okt  9 13:44
        virtual_hosting                        0  Okt  9 13:44
dav:/> 
```

This works like a charm, and it is fun!

You get the command reference via `help`.
```
dav:/> help
Available commands: 
 ls         cd         pwd        put        get        mget       mput       
 edit       less       mkcol      cat        delete     rmcol      copy       
 move       lock       unlock     discover   steal      showlocks  version    
 checkin    checkout   uncheckout history    label      propnames  chexec     
 propget    propdel    propset    search     set        open       close      
 echo       quit       unset      lcd        lls        lpwd       logout     
 help       describe   about      
Aliases: rm=delete, mkdir=mkcol, mv=move, cp=copy, more=less, quit=exit=bye
```

## Disclaimer

Usually, it is a good idea to directly edit the project's documentation instead of writing a blog post or a til.

I will try to submit a PR to amend the documentation.

## Further resources

Documentation on how to activate WebDav for Zope, scroll down to `webdav-source-port`
https://zope.readthedocs.io/en/latest/operation.html#zope-configuration-reference

Cadaver WebDav client: http://www.webdav.org/cadaver/

## Udpate 2020-10-09

Also **Nautilus**, the file explorer for Gnome/Ubuntu, supports the **WebDav** protocol!
