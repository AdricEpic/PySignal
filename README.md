# PySignal

A Qt style signal implementation that doesn't require QObjects.
This supports class methods, functions, lambdas and partials.

Signals can either be created on the instance or on the class, and can be handled either as objects or by string name.
Unlike PyQt signals, PySignals do not enforce types by default as I believe this is more pythonic.

## Install

You can install this using pip

```bash
pip install PySignal
```

This is compatible with Python 2.7+ and 3.x

## Usage:

```python
def greet(name):
    print "Hello,", name

class Foo(object):
    started = ClassSignal()

    def __init__(self):
        super(Foo, self).__init__()
        self.started.connect(greet)
        self.started.emit('Watson')

        self.signalFactory = SignalFactory()
        self.signalFactory.register('Greet')
        self.signalFactory['Greet'].connect(greet)
        self.signalFactory['Greet'].emit('Sherlock')

foo = Foo()
# Hello, Watson
# Hello, SHerlock
```

## Signal Types

There are 4 types of Signals included

* `Signal` is the base implementation of the Signal and can be created on a per instance level.
* `ClassSignal` is an object that can be created as a class variable and will act like a signal.
    This ensures that all instances of your class will have the signal, but can be managed individually.
* `SignalFactory` allows you to have a single signal object on your class that can generate signals by name.
* `ClassSignalFactory` is the same as a signal factory but lives on the class instead of the instance.

## Based on these implementations

http://www.jnvilo.com/cms/programming/python/programming-in-python/signal-and-slots-implementation-in-python

http://www.codeheadwords.com/2015/05/05/emulating-pyqt-signals-with-descriptors