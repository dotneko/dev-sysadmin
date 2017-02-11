*Notes from Coursera Using Databases with Python by Prof. Charles Severance*

# Basic Structure / Syntax
```
class ClassName:
    x = 0

    def methodName(self):
        self.x = self.x + 1

anObj = ClassName()

anObj.methodName();
```

- `self` is a variable that is an alias to an instance.
- Each instance has to have one parameter if want objects to "talk" to each other.

### `type()`
- `type(anObj)` returns something about the variable/object.

### `dir()`
- `dir(anObj)` lists capabilities of a class.
- Items enclosed by underscores are reserved methods used by Python.

# Object Lifecycle

- Objects are created, used and discarded
- Constructors are methods that sets up instance variables that have initial values.
- Destructors are rarely used.

```
class ClassName:

    def __init__(self, nam):
        self.name = nam

    def __del__(self):
        ...
```

# Inheritance

- Using an existing class in which one inherits all the capabilities of an existing class. Other terms are extending the class.
- Syntax:

```
class Class1:
    x = 0
    name = ""
    def __init__(self,nam):
        ...
    def a_Method(self):
        ...

class Class2(Class1):
    ...
```
