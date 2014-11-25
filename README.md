xivo-dird-client
================

A python library to connect to xivo-dird.

Usage:

```python
from xivo_dird_client import Client

c = Client('localhost', port=9489, version='0.1')

results = c.directories.lookup(profile='default', term='alice')

# or

results = c.directories.lookup.default(term='alice')
```


## How to implement a new command

Someone trying to implement a new command to the client would have to implement
a new class sub-classing the BaseHTTPCommand. The new class must be in the
setup.py in the entry points under dird_client.commands. The name of the entry
point is used as the handle on the client. For example, if you new entry point
entry looks like this:

```python
entry_points={
    'dird_client.commands': [
        'foo = package.to.foo:FooCommand'
    ]
}
```

your command will be accessible from the client like this:

```python
c = Client(...)

c.foo.bar()  # bar is a method of the FooCommand class
```
