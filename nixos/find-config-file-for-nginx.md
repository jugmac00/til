# Find config file for nginx

Nixos... hm, a dream for my hoster, but a nightmare as a casual user :-D

Compared to other Linux distros, there are so many differences.

For a start... where the heck is my `nginx.conf`? Hint - it is not in `/etc/nginx/nginx.conf`

```
systemctl cat nginx

...
X-CheckConfigCmd=/nix/store/xxx-nginx-1.14.2/bin/nginx -t -c /nix/store/xxx-nginx.conf -p /var/spool/nginx
X-ConfigFile=/nix/store/xxx-nginx.conf
```

In order to show the configuration, FlyingCircus (my hoster) created a custom command

```
nginx-show-config | less
...
```

This outputs the combined nginx configuration.
