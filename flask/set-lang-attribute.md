# How can you inject the language into a Jinja template so you can set it as a lang attribute?

I created a mulitlingual project using Flask with the help of Flask-Babel.

While the translation mechanism via GNU gettext itself is pretty straightforward, I did not know how to inject the actual language into the Jinja template, so I can use it to set `<html lang="xxx">`.

While it is odd that this is not mentioned in the documenation, once again StackOverflow offered solutions.

## solution one

Just translate the language!

```
<html lang="{{ _('en') }}">
```

That was too simple to think of :-)

## solution two

Inject it into the context.

```
babel = Babel(app)
...
@app.context_processor
def utility_processor():
    return dict(lang=babel.locale_selector_func())
...

<html lang="{{ lang }}">
```

via https://stackoverflow.com/questions/53832101/set-html-tag-lang-attribute-accordingly-using-flask-babel
