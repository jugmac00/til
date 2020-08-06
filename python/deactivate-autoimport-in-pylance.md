# How to deactivate autoimport in PyLance?

Unfortunately, the **autoimport** feature in PyLance surprised me with `random` imports.

e.g. with `from unittest.case import expectedFailure` just when I typed `assert result == expected`.

Luckily, the developers heard on the users, and with version 2020.8.0 this "feature" is optional.

In order to deactivate it, set the following option to `false`:

```
python.analysis.autoImportCompletions
```

Thank you, Savannah!
