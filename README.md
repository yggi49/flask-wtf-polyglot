Flask-WTF-Polyglot
==================

[Flask-WTF][1] companion library providing `PolyglotForm` for [polyglot
HTML][2] output.

Polyglot markup is a set of rules for how to write HTML.  A document that uses
polyglot markup is both a valid HTML5 document as well as a well-formed XML
document, that can be served with either a `text/html` or an
`application/xhtml+xml` MIME type.

This package provides the `PolyglotForm` class, which is built on top of
Flask-WTF’s default `Form`.  When using `PolyglotForm`, fields will be
rendered with polyglot markup.  For example, given the following form:

```python
from flask_wtf_polyglot import PolyglotForm
from wtforms import BooleanField

class MyForm(PolyglotForm):
    foo = BooleanField("foo", default=True)
```

Rendering `MyForm.foo` will result in the following XML-compliant output:

```html
<input checked="checked" id="foo" name="foo" type="checkbox" value="y" />
```

In contrast, using Flask-WTF’s default `Form`, the output would be:

```html
<input checked id="foo" name="foo" type="checkbox" value="y">
```

In addition, this package exports `WTForms-Polyglot`_’s custom implementation
of WTForms’ `SubmitField`, which renders as a `<button>` instead of an
`<input>` element.  For example:

```python
from flask_wtf_polyglot import PolyglotForm, SubmitField

class MyForm(PolyglotForm):
    foo = SubmitField('Bar')
```

Produces this output:

```html
<button id="foo" name="foo" type="submit" value="bar">bar</button>
```


Dependencies
------------

Apart from Flask-WTF, this package relies upon [WTForms-Polyglot][3] to
produce polyglot markup.

[1]: https://flask-wtf.readthedocs.io/
[2]: http://www.w3.org/TR/html-polyglot/
[3]: https://pypi.python.org/pypi/WTForms-Polyglot/
