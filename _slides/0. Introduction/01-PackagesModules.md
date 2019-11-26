# Packages and Modules

---
### Packages and Modules

- Overview
- The Module Search Path
- The import Statement
- The dir() Function
- Executing a Module as a Script
- Reloading a Module
- Python Packages
- Package Initialization
- Importing * From a Package
- Subpackages


---
### Overview

Modular programming refers to the process of breaking a large, unwieldy programming task into separate, smaller, more manageable subtasks or modules

Individual modules can then be cobbled together like building blocks to create a larger application

---
### Advantages
There are several advantages to modularizing code in a large application
- Simplicity: focus on one relatively small portion of the problem
- Maintainability: they enforce logical boundaries between different problem domains
- Reusability: functionality defined in a single module can be easily reused
- Scoping: modules typically define a separate namespace, which helps avoid collisions between identifiers in different areas of a program

Functions, modules and packages are all constructs in Python that promote code modularization.

---
### Module definitions
There are actually three different ways to define a module in Python:

- A module can be written in Python itself
- A module can be written in C and loaded dynamically at run-time, like the re (regular expression) module
- A built-in module is intrinsically contained in the interpreter, like the itertools module

---
### Module definitions (2)
A module’s contents are accessed the same way in all three cases
- with the import statement

To create a module
- create a file that contains legitimate Python code 
- give the file a name with a .py extension

That’s it! 

---
###  Module Example

suppose you have created a file called mod.py containing the following:
```
s = "If Comrade Napoleon says it, it must be right."
a = [100, 200, 300]

def foo(arg):
    print(f'arg = {arg}')

class Foo:
    pass
```

Several objects are defined in mod.py:
- s (a string)
- a (a list)
- foo() (a function)
- Foo (a class)

---
### Module Example (2)

Assuming mod.py is in an appropriate location, which you will learn more about shortly, these objects can be accessed by importing the module as follows:
```
>>> import mod
>>> print(mod.s)
If Comrade Napoleon says it, it must be right.
>>> mod.a
[100, 200, 300]
>>> mod.foo(['quux', 'corge', 'grault'])
arg = ['quux', 'corge', 'grault']
>>> x = mod.Foo()
>>> x
<mod.Foo object at 0x03C181F0>
```


---
### The Module Search Path
Take a look at what happens when Python executes the statement:
```
import mod
```
When the interpreter executes the above import statement, it searches for mod.py in a list of directories:
- directory from which the input script was run or the current directory if the interpreter is being run interactively
- list of directories contained in the PYTHONPATH environment variable, if it is set. 
- an installation-dependent list of directories configured at the time Python is installed

---
### The Module Search Path (2)

The resulting search path is accessible in the Python variable sys.path, which is obtained from a module named sys:
```
>>> import sys
>>> sys.path
['', 'C:\\Users\\john\\Documents\\Python\\doc', 'C:\\Python36\\Lib\\idlelib',
'C:\\Python36\\python36.zip', 'C:\\Python36\\DLLs', 'C:\\Python36\\lib',
'C:\\Python36', 'C:\\Python36\\lib\\site-packages']
```

Note: The exact contents of sys.path are installation-dependent. The above will almost certainly look slightly different on your computer

---
### The Module Search Path (3)
Thus, to ensure your module is found, you need to do one of the following:
- put mod.py in the directory where the input script is located or the current directory, if interactive
- modify the PYTHONPATH environment variable to contain the directory where mod.py is located before starting the interpreter
or: put mod.py in one of the directories already contained in the PYTHONPATH variable
- put mod.py in one of the installation-dependent directories, which you may or may not have write-access to, depending on the OS

---
### The Module Search Path (4)

You can put the module file in any directory of your choice and then modify sys.path at run-time so that it contains that directory. 

For example, in this case, you could put mod.py in directory C:\Users\john and then issue the following statements:
```
>>> sys.path.append(r'C:\Users\john')
>>> sys.path
['', 'C:\\Users\\john\\Documents\\Python\\doc', 'C:\\Python36\\Lib\\idlelib',
'C:\\Python36\\python36.zip', 'C:\\Python36\\DLLs', 'C:\\Python36\\lib',
'C:\\Python36', 'C:\\Python36\\lib\\site-packages', 'C:\\Users\\john']
>>> import mod
```

---
### The Module Search Path (5)
Once a module has been imported, you can determine the location where it was found with the module’s __file__ attribute:
```
>>> import mod
>>> mod.__file__
'C:\\Users\\john\\mod.py'

>>> import re
>>> re.__file__
'C:\\Python36\\lib\\re.py'
```

The directory portion of __file__ should be one of the directories in sys.path

---
### The import Statement 
Module contents are made available to the caller with the import statement. 

The import statement takes many different forms, shown below.
- import module_name
  - this does not make the module contents directly accessible to the caller
  - objects in the module are only accessible when prefixed with module_name via dot notation
- from module_name import name [as alt_name]
  - alternate form of the import statement allows individual objects from the module to be imported directly into the caller’s symbol table
  - it is also possible to import individual objects but enter them into the local symbol table with alternate names
- from module_name import *
  - this will place the names of all objects from module_name into the local symbol table
  - with the exception of any that begin with the underscore (_) character

---
### Some Examples
```
>>> import mod
>>> mod.s
'If Comrade Napoleon says it, it must be right.'
>>> mod.foo('quux')
```

```
>>> from mod import s, foo
>>> s
'If Comrade Napoleon says it, it must be right.'
>>> foo('quux')
```

```
>>> from mod import *
>>> s
'If Comrade Napoleon says it, it must be right.'
>>> a
[100, 200, 300]
>>> foo
<function foo at 0x03B449C0>
>>> Foo
<class 'mod.Foo'>
```

---
### The import Statement (2)

Python 3 does not allow the indiscriminate import * syntax from within a function:
```
>>> def bar():
...     from mod import *
...
SyntaxError: import * only allowed at module level
```

---
### The import Statement (3)
A try statement with an except ImportError clause can be used to guard against unsuccessful import attempts:
```
>>> try:
...     # Non-existent module
...     import baz
... except ImportError:
...     print('Module not found')
...
```
Module not found
```
>>> try:
...     # Existing module, but non-existent object
...     from mod import baz
... except ImportError:
...     print('Object not found in module')
...
```
Object not found in module


---
### The dir() Function
The built-in function dir() returns a list of defined names in a namespace 

Without arguments, it produces an alphabetically sorted list of names in the current local symbol table:
```
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__']

>>> qux = [1, 2, 3, 4, 5]
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__', 'qux']

>>> class Bar():
...     pass
...
>>> x = Bar()
>>> dir()
['Bar', '__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__', 'qux', 'x']
```

Note how the first call to dir() above lists several names that are automatically defined and already in the namespace when the interpreter starts

As new names are defined (qux, Bar, x), they appear on subsequent invocations of dir()

---
### The dir() Function(2)
When given an argument that is the name of a module, dir() lists the names defined in the module:
```
>>> import mod
>>> dir(mod)
['Foo', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__',
'__name__', '__package__', '__spec__', 'a', 'foo', 's']
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__']
>>> from mod import *
>>> dir()
['Foo', '__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__', 'a', 'foo', 's']
```

---
### Executing a Module as a Script
Any .py file that contains a module is essentially also a Python script
- Unfortunately, it could generate output when imported as a module
```
>>> import mod
If Comrade Napoleon says it, it must be right.
[100, 200, 300]
```
This is probably not what you want. It isn’t usual for a module to generate output when it is imported

Wouldn’t it be nice if you could distinguish between when the file is loaded as a module and when it is run as a standalone script?

---
### Executing a Module as a Script
When a .py file is imported as a module
- Python sets the special dunder variable __name__ to the name of the module
If a file is run as a standalone script
- __name__ is (creatively) set to the string '__main__'

alter behavior accordingly:
```
s = "If Comrade Napoleon says it, it must be right."
a = [100, 200, 300]

def foo(arg):
    print(f'arg = {arg}')

class Foo:
    pass

if (__name__ == '__main__'):
    print('Executing as standalone script')
    print(s)
    print(a)
    foo('quux')
    x = Foo()
    print(x)
```

Now, if you run as a script, you get output, imported as a module, no output

---
### Executing a Module as a Script
Modules are often designed with the capability to run as a standalone script for purposes of testing the functionality that is contained within the module 
This is referred to as unit testing. 

For example
```
def fact(n):
    return 1 if n == 1 else n * fact(n-1)

if (__name__ == '__main__'):
    import sys
    if len(sys.argv) > 1:
        print(fact(int(sys.argv[1])))
```

The file can be treated as a module, and the fact() function imported:

```
>>> from fact import fact
>>> fact(6)
720
```

But it can also be run as a standalone by passing an integer argument on the command-line for testing:
```
C:\Users\john\Documents>python fact.py 6
720
```

---
### Reloading a Module
For reasons of efficiency
- a module is only loaded once per interpreter session

Consider the following file mod.py:
```
a = [100, 200, 300]
print('a =', a)
```
```
>>> import mod
a = [100, 200, 300]
>>> import mod
>>> import mod

>>> mod.a
[100, 200, 300]
```

The print() statement is not executed on subsequent imports.

---
### Reloading a Module
If you make a change to a module and need to reload it, you need to either 
- restart the interpreter or 
- use a function called reload() from module importlib

```
>>> import mod
a = [100, 200, 300]

>>> import mod

>>> import importlib
>>> importlib.reload(mod)
a = [100, 200, 300]
<module 'mod' from 'C:\\Users\\john\\Documents\\Python\\doc\\mod.py'>
```

---
### Python M command line option
When you use the -m command-line flag, Python will import a module or package for you, then run it as a script.

When you don't use the -m flag, the file you named is run as just a script

There is a big difference between:
- python foo/bar/baz.py and python -m foo.bar.baz

in the latter case, foo.bar is imported and relative imports will work correctly with foo.bar as the starting point.

---
<!-- .slide: data-background="url('images/demo.jpg')" data-background-size="cover" --> 
<!-- .slide: class="lab" -->
## Demo time!
Modules


---
### Python Packages
Packages 
- allow grouping and organizing modules
- allow for a hierarchical structuring of the module namespace using dot notation

In the same way that modules help avoid collisions between global variable names, packages help avoid collisions between module names

---
### Creating Python Packages
Creating a package is quite straightforward
- it makes use of the operating system’s inherent hierarchical file structure

Consider the following arrangement:

Here, there is a directory named pkg that contains two modules, mod1.py and mod2.py. The contents of the modules are:
```
pkg\mod1.py

def foo():
    print('[mod1] foo()')

class Foo:
    pass
```
```
pkg\mod2.py

def bar():
    print('[mod2] bar()')

class Bar:
    pass
```

Given this structure, if the pkg directory resides in a location where it can be found 
you can refer to the two modules with dot notation (pkg.mod1, pkg.mod2) and import them with the syntax you are already familiar with:

---
### Creating Python Packages (2)
```
>>> import pkg.mod1, pkg.mod2
>>> pkg.mod1.foo()
[mod1] foo()
>>> x = pkg.mod2.Bar()
>>> x
<pkg.mod2.Bar object at 0x033F7290>
```
```
>>> from pkg.mod1 import foo
>>> foo()
[mod1] foo()
from <module_name> import <name> as <alt_name>
>>> from pkg.mod2 import Bar as Qux
>>> x = Qux()
>>> x
<pkg.mod2.Bar object at 0x036DFFD0>
```

---
### Creating Python Packages (3)
You can technically import the package as well:
```
>>> import pkg
>>> pkg
<module 'pkg' (namespace)>
```

But this is of little avail. Though this is, strictly speaking, a syntactically correct Python statement, it doesn’t do much of anything useful. 
In particular, it does not place any of the modules in pkg into the local namespace:
```
>>> pkg.mod1
Traceback (most recent call last):
  File "<pyshell#34>", line 1, in <module>
    pkg.mod1
AttributeError: module 'pkg' has no attribute 'mod1'
>>> pkg.mod1.foo()
Traceback (most recent call last):
  File "<pyshell#35>", line 1, in <module>
    pkg.mod1.foo()
AttributeError: module 'pkg' has no attribute 'mod1'
>>> pkg.mod2.Bar()
Traceback (most recent call last):
  File "<pyshell#36>", line 1, in <module>
    pkg.mod2.Bar()
AttributeError: module 'pkg' has no attribute 'mod2'
```

To actually import the modules or their contents, you need to use one of the forms shown above.

---
### Package Initialization
If a file named __init__.py is present in a package directory
- it is invoked when the package or a module in the package is imported

This can be used for execution of package initialization code, such as initialization of package-level data

---
### Package Initialization (2)
For example, consider the following __init__.py file:

pkg\__init__.py
```
print(f'Invoking __init__.py for {__name__}')
A = ['quux', 'corge', 'grault']
```

Now when the package is imported, global list A is initialized:
```
>>> import pkg
Invoking __init__.py for pkg
>>> pkg.A
['quux', 'corge', 'grault']
```

---
### Package Initialization (3)
A module in the package can access the global by importing it in turn:

pkg\mod1.py
```
def foo():
    from pkg import A
    print('[mod1] foo() / A = ', A)

class Foo:
    pass
```
```
>>> from pkg import mod1
Invoking __init__.py for pkg
>>> mod1.foo()
[mod1] foo() / A =  ['quux', 'corge', 'grault']
```

---
### Package Initialization (3)
__init__.py can also be used to effect automatic importing of modules from a package

For example, earlier you saw that the statement import pkg only places the name pkg in the caller’s local symbol table and doesn’t import any modules
if __init__.py in the pkg directory contains the following:

pkg\__init__.py
```
print(f'Invoking __init__.py for {__name__}')
import pkg.mod1, pkg.mod2
```

when you execute import pkg, modules mod1 and mod2 are imported automatically:
```
>>> import pkg
Invoking __init__.py for pkg
>>> pkg.mod1.foo()
[mod1] foo()
>>> pkg.mod2.bar()
[mod2] bar()
```

---
### Package Initialization (4)

Much of the Python documentation states that an __init__.py file must be present in the package directory when creating a package
- this was once true. 
- this file could contain initialization code or even be empty, but it had to be present

Starting with Python 3.3
- implicit Namespace Packages were introduced
- allow for the creation of a package without any __init__.py file
- it can still be present if package initialization is needed
- no longer required

---
### Importing * From a Package
When import * is used for a module, all objects from the module are imported into the local symbol table, except those whose names begin with an underscore

The analogous statement for a package is this:
- from package_name import *

What does that do?

---
### Importing * From a Package (2)
```
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__']

>>> from pkg import *
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__']
```

Hmph. Not much

Python follows this convention
- if the __init__.py file in the package directory contains a list named __all__, it is taken to be a list of modules that should be imported when the statement from package_name import * is encountered

---
### Importing * From a Package (3)
Suppose you create an __init__.py in the pkg directory like this:
```
pkg/__init__.py

__all__ = [
        'mod1',
        'mod2',
        'mod3',
        'mod4'
        ]
```

Now from pkg import * imports all four modules:
```
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__']

>>> from pkg import *
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__', 'mod1', 'mod2', 'mod3', 'mod4']
>>> mod2.bar()
[mod2] bar()
>>> mod4.Qux
<class 'pkg.mod4.Qux'>
```

---
### Importing * From a Package (4)
Using import * still isn’t considered terrific form, any more for packages than for modules. 
- at least gives the creator of the package some control over what happens when import * is specified

By the way, __all__ can be defined in a module as well and serves the same purpose: 
- to control what is imported with import *. For example, modify mod1.py as follows:

---
### Importing * From a Package (5)
pkg/mod1.py
```
__all__ = ['foo']

def foo():
    print('[mod1] foo()')

class Foo:
    pass
```

Now an import * statement from pkg.mod1 will only import what is contained in __all__:
```
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__']

>>> from pkg.mod1 import *
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__',
'__package__', '__spec__', 'foo']
```

```
>>> foo()
[mod1] foo()
>>> Foo
Traceback (most recent call last):
  File "<pyshell#37>", line 1, in <module>
    Foo
NameError: name 'Foo' is not defined
```


---
### All Summary
In summary, __all__ is used by both packages and modules to control what is imported when import * is specified

But the default behavior differs:
- For a package, when __all__ is not defined, import * does not import anything
- For a module, when __all__ is not defined, import * imports everything (except—you guessed it—names starting with an underscore)

---
### Subpackages
Packages can contain nested subpackages to arbitrary depth 

For example, let’s make one more modification to the example package directory as follows:
- four modules (mod1.py, mod2.py, mod3.py and mod4.py) are defined as previously
- they are split out into two subpackage directories, sub_pkg1 and sub_pkg2

Importing still works the same as shown previously

---
### Subpackages (2)

Syntax is similar, but additional dot notation is used to separate package name from subpackage name:
```
>>> import pkg.sub_pkg1.mod1
>>> pkg.sub_pkg1.mod1.foo()
[mod1] foo()

>>> from pkg.sub_pkg1 import mod2
>>> mod2.bar()
[mod2] bar()

>>> from pkg.sub_pkg2.mod3 import baz
>>> baz()
[mod3] baz()

>>> from pkg.sub_pkg2.mod4 import qux as grault
>>> grault()
[mod4] qux()
```

---
### Import
In addition, a module in one subpackage can reference objects in a sibling subpackage

For example, suppose you want to import and execute function foo() (defined in module mod1) from within module mod3. 

You can either use an absolute import or a relative one

---
### Absolute import (2)


pkg/sub__pkg2/mod3.py
```
def baz():
    print('[mod3] baz()')

class Baz:
    pass

from pkg.sub_pkg1.mod1 import foo
foo()

>>> from pkg.sub_pkg2 import mod3
[mod1] foo()
>>> mod3.foo()
[mod1] foo()
```

---
### Relative import

.. refers to the package one level up. 

From within mod3.py, which is in subpackage sub_pkg2
- .. evaluates to the parent package (pkg), and
- ..sub_pkg1 evaluates to subpackage sub_pkg1 of the parent package

pkg/sub__pkg2/mod3.py
```
def baz():
    print('[mod3] baz()')

class Baz:
    pass

from .. import sub_pkg1
print(sub_pkg1)

from ..sub_pkg1.mod1 import foo
foo()
>>> from pkg.sub_pkg2 import mod3
<module 'pkg.sub_pkg1' (namespace)>
[mod1] foo()
```


---
<!-- .slide: data-background="url('images/demo.jpg')" data-background-size="cover" --> 
<!-- .slide: class="lab" -->
## Demo time!
Packages

---
<!-- .slide: data-background="url('images/lab2.jpg')" data-background-size="cover"  --> 
<!-- .slide: class="lab" -->
## Lab time!
Creating Packages and Modules
