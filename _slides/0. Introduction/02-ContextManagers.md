# Context Managers

---
### Context Managers
Motivation
- Resource Management

The most straightforward way to accomplish proper resource management would be calling the close function after we're done with the resource.

For example:
```
opened_file = open('readme.txt')
text = opened_file.read()
...
opened_file.close()
```

---
### Context Managers (2)

Now at first glance this might seem okay, but actually, it's not robust at all. 
- if anything unexpected happens between opening the file and closing the file, there would be a resource leak
 
These unexpected events are what we call exceptions, a common one would be when someone forcefully closes the program while it's executing.

---
### Context Managers (2)
The proper way to handle this would be using Exception handling, using try...else blocks. 

Look at the following example:
```
try:
    opened_file = open('readme.txt')
    text = opened_file.read()
    ...
else:
    opened_file.close()
```

Python always makes sure the code in the else block is executed, regardless of anything that might happen

---
### Implementing Context Managers
The standard and "lower-level" way of implementing a context manager is defining two "magic" methods in the class you want to implement resource management for
- __enter__ is the method that gets called when we open the resource
- __exit__ contains clean-up code which must be executed after we're done with the resource, no matter what.


```
class FileManager:
    def __init__(self, filename):
        self.filename = filename
        
    def __enter__(self):
        self.opened_file = open(self.filename)
        return self.opened_file

    def __exit__(self. *exc):
        self.opened_file.close()
```


---
### Using Context Managers

```
file = FileManager('readme.txt')
with file as managed_file:
    text = managed_file.read()
    print(text)
with FileManager('readme.txt') as managed_file:
    text = managed_file.read()
    print(text)
def open_file(filename):
    file = FileManager(filename)
    return file

with open_file('readme.txt') as managed_file:
    text = managed_file.read()
    print(text)
```

---
### Using contextlib
There is a library named contextlib containing utilities regarding context managers
```
from contextlib import contextmanager

@contextmanager
def open_file(filename):
    opened_file = open(filename)
    try:
        yield opened_file
    finally:
        opened_file.close()
```

All the contents you'd otherwise put in the __enter__ method, except the return statement, goes before the try block here 
- instead of returning the resource, you yield it, inside a try block.

The contents of the __exit__ method goes inside the corresponding finally block.

Once we have such a function, we can decorate it using the contextlib.contextmanager decorator and we're good

---
### Using contextlib example

```
with open_file('readme.txt') as managed_file:
    text = managed_file.read()
    print(text)
```

As you can see, the decorated open_file function returns a context manager and we can use that directly.


---
<!-- .slide: data-background="url('images/demo.jpg')" data-background-size="cover" --> 
<!-- .slide: class="lab" -->
## Demo time!
Context Managers

---
<!-- .slide: data-background="url('images/lab2.jpg')" data-background-size="cover"  --> 
<!-- .slide: class="lab" -->
## Lab time!
Context Managers



