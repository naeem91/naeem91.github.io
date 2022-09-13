---
title: "Introspecting Python Functions"
date: 2022-09-13T18:49:50+05:00
draft: false
categories: ["Python"]
---

### Functions are objects
Since everything in Python is an object so are functions. They are instances of class `<class 'function'>` and have properties and methods attached to them.

Let's define a simple function and play with its properties:
```python
>>> def square(x:int = 0) -> int: return x**2
...
>>> dir(square)
['__annotations__', '__builtins__', '__call__', '__class__', '__closure__', '__code__', '__defaults__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__get__', '__getattribute__', '__globals__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__kwdefaults__', '__le__', '__lt__', '__module__', '__name__', '__ne__', '__new__', '__qualname__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__']
>>> square.__annotations__
{'x': <class 'int'>, 'return': <class 'int'>}
>>> square.__class__
<class 'function'>
```

### Building a type validator for function arguments
One interesting experiment I did was to create a very simple type checker that validates values against the annotated types using function introspection techniques.

Our type checker is a decorator that is applied to a function with type annotations:

```python
import inspect


def type_validator(fn):
    type_annots = fn.__annotations__

    def wrapper(*args, **kw):
        values = inspect.getcallargs(fn, *args, **kw)
        for arg, val in values.items():
            arg_type = type_annots.get(arg)
            if  arg_type is not None and not isinstance(val, arg_type):
                raise ValueError(f'{arg} expects type {arg_type}, found {type(val)}')

        return fn(*args, **kw)

    return wrapper


@type_validator
def square(x: int) -> int: 
    return x**2

```
Let's run the `square` methods with some inputs:

```python
>>> square(10.0)
ValueError: x expects type <class 'int'>, found <class 'float'>
>>> square('abc')
ValueError: x expects type <class 'int'>, found <class 'str'>'
>>> square(10)
100
```