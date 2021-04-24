# How to test log output with `zope.testrunner`?

While `pytest` makes it very easy to work with logfiles via the [caplog fixture](https://docs.pytest.org/en/latest/how-to/logging.html#caplog-fixture),
I was not aware how to test them with `zope.testrunner`, which is used for almost all Zope repositories.

When I asked during yesterday's Zope sprint, I got no answer.

But coincidentally, I stumbled upon a broken doctest which... tests the log output of a function!

So... thanks for failing ...I guess :-)

You need to setup a log handler, which captures the log messages...
```
>>> import zope.testing.loggingsupport
>>> handler = zope.testing.loggingsupport.InstalledHandler('ZEO', level=logging.ERROR)
```

... and then you can inspect the list of log records...
```
>>> handler.records
```

Do not forget to clean up afterwards!

```
>>> handlers.uninstall()  # remove handler(s), and thus stop collecting log records
>>> handlers.clear()  # delete collected log records
```

## update

2021.04.24:
- added missing teardown instructions - thanks to [Marius](https://twitter.com/mgedmin/status/1385969813449756672) for pointing out!
