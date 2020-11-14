# how can you group data easily with `SimpleNamespace`?

While you could use the usual suspects, like `dicts`, `NamedTuple`, `dataclasses` or even an "empty" class, there is yet another way: `SimpleNamespace`.

```
>>> from types import SimpleNamespace
>>> simple_ns = SimpleNamespace(a=1, b="two")
>>> simple_ns
namespace(a=1, b='two')
>>> simple_ns.a
1
>>> simple_ns.b
'two'
>>> 

```

## implementation

This `builtin` is [implemented in C](https://github.com/python/cpython/blob/3.9/Objects/namespaceobject.c),
but the [Python docs](https://docs.python.org/3/library/types.html?highlight=simplenamespace#types.SimpleNamespace) show how it would look like in Python:

```
class SimpleNamespace:
    def __init__(self, /, **kwargs):
        self.__dict__.update(kwargs)

    def __repr__(self):
        items = (f"{k}={v!r}" for k, v in self.__dict__.items())
        return "{}({})".format(type(self).__name__, ", ".join(items))

    def __eq__(self, other):
        return self.__dict__ == other.__dict__
```

That is the reason why we have this nice representation.

```
>>> simple_ns
namespace(a=1, b='two')
```

As a plus, you can even compare instances by attribute comparison, and not only by `id`!

```
>>> another_ns = SimpleNamespace(a=1, b="two")
>>> simple_ns == another_ns
True
>>> simple_ns is another_ns
False
```

## why not a class?

```
>>> class NS:
...     pass
... 
>>> class_ns = NS()
>>> class_ns.a = 1
>>> class_ns.b = "two"
>>> class_ns
<__main__.class_ns object at 0x7f01cc670c18>

>>> another_class_ns = NS()
>>> another_class_ns.a = 1
>>> another_class_ns.b = "two"
>>> class_ns == another_class_ns
False
>>> 
```

### fun fact

When you have a look at the above implementation, it looks like only the dictionaries are compared - but this is not true:

```
>>> simple_ns == class_ns
False
```

The reason is simple. The above Python implementation is not complete.

The C implemenation also does a type check.

```
static PyObject *
namespace_richcompare(PyObject *self, PyObject *other, int op)
{
    if (PyObject_IsInstance(self, (PyObject *)&_PyNamespace_Type) &&
            PyObject_IsInstance(other, (PyObject *)&_PyNamespace_Type))
        return PyObject_RichCompare(((_PyNamespaceObject *)self)->ns_dict,
                                   ((_PyNamespaceObject *)other)->ns_dict, op);
    Py_INCREF(Py_NotImplemented);
    return Py_NotImplemented;
}
```

I created a [bug report at the cpython issue tracker](https://bugs.python.org/issue42344),
let's see what the core developers think about it.
**Update 2020-11-14** My [pull request](https://github.com/python/cpython/pull/23264) was merged.

## why not just object?

```
>>> obj = object()
>>> obj
<object object at 0x7f01cddfe3c0>
>>> obj.a = 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'object' object has no attribute 'a'
```

So, there are several reasons, but reason nr. 1 is, you cannot add attributes.

## thanks

Thanks Anthony Sottile for sharing his video [easy fake objects with python's SimpleNamespace](https://www.youtube.com/watch?v=8XvyHj8ndg8&ab_channel=anthonywritescode)
