# How can I view log entries when using systemd?

Until very recently I was lucky enough to have real logfiles, but now I have to use systemd's way to view logs.

## show all log entries

```
journalctl
```

## show Nginx' log entries

```
journalctl -u nginx
```

## directly jump to the latest entries

```
journalctl -e -u nginx
```
