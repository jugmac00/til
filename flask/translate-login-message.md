# How can you access the login message in order to translate it?

When you use **Flask-Login**, the default login message comes from the plugin.

This means - you do no set it, you cannot translate it.

## solution

Set the very same (or a different) message!

```
login = LoginManager(app)
login.login_view = 'login'
login.login_message = _l('Please log in to access this page.')
```

via https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-xiii-i18n-and-l10n
