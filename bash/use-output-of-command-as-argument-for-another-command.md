# TIL my TIL is not secure

There is a security issue with the following description - at least when you handle sensitive data.

see here
https://github.com/jugmac00/til/commit/7ea93202cecf97070c8931bbe5a1f64c78d41dcb#commitcomment-42050997

Thanks to @asottile for reporting!

Please see https://unix.stackexchange.com/questions/205180/how-to-pass-password-to-mysql-command-line for a better way to create a login one-liner.


## How do you use the output of one bash command as an argument for another command?

At my hoster ( https://flyingcircus.io/ ), the `mysql` root password is stored in a config file.

Whenever I need to login as root, I do the following steps:

```
cat /etc/local/mysql/mysql.passwd
# copy the output
mysql -u root - p  # hit enter
# paste the output
```
I do not paste the password directly after the `-p` so it does not get stored in the bash history.

All in all, pretty inconvenient.

### There must be a better way

We all know pipes ( `ls | grep search_term` ), but here we need the output as an argument.

While we could assign the output to a variable, there is an easier way.

```
mysql -u root -p"$(cat /etc/local/mysql/mysql.passwd)"
```

The above command reads the password from the configuration file and directly uses it as input for the `mysql` command.

The correct term for this is **command substitution**.

## Further information

https://tldp.org/LDP/abs/html/commandsub.html
