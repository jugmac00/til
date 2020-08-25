# How can you sort files/folders in Nautilus so folders gets shown first?

## update settings

```
gsettings set org.gtk.Settings.FileChooser sort-directories-first true
```

## check settings

```
gsettings get org.gtk.Settings.FileChooser sort-directories-first
```

via https://askubuntu.com/questions/1064482/
