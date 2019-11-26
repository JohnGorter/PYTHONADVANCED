# Descriptors


---
### Descriptors

A class that implements a get, set or delete methods for an object is called descriptors.

Descriptors are the way to create attributes and add managed attributes to objects
- these are used to protect the attributes from changes and any modifications
- descriptors can able to increase the readability of a program and coding skills
- they can help to validate the data

For example, suppose we need only positive integer values for attribute age and string values for attribute string

---
### Descriptor Protocol
To create a descriptor, we need a descriptor protocol. By defining the following methods we can efficiently manage the attributes. They are:

    __get__(self, obj, type=None)
    __set__(self, obj, value)
    __delete__(self, obj)

- __get__ : It gets the value from an object and returns it.
- __set__ : It sets a value to the object and returns none.
- __delete__ : It deletes the value in the object and return none.

These methods are normally referred to as getter and setter methods\

---
### Creating and calling Descriptors
We can create a descriptor in many ways:
- create a class and override any of the __get__, __set__ and __delete__ methods and use them
- use the property type to create descriptor
- by combining both property type and python decorators

Let look at each way of creating descriptor

---
### Creating descriptors using class
```
class rk:
	def __init__(self):
		self.value=0
		
	def __get__(self,ob, ty):
		print ("get method")		
		return self.value
		
	def __set__(self, ob, ty):
		self.value = ty
		print("set method",self.value)
	
	def __delete__(self, ob):	
		print("delete method")
		del self.value

class inc:
	r=rk()
	
a=inc()
print(a.r)
a.r=3
del a.r
Output

get method
0
set method 3
delete method
```

In the above program 
- the get method will __get__ the value, 
- the __set__ method will set the value to attribute 
- the __delete__ method will delete the attribute

---
### Creating descriptor using property type
By using property() it is easy to create descriptors.

Syntax for creating a property method is:
```
    property(fget=None, fset=None, fdel=None, doc=None)
```

fget : Function to be used for getting an attribute value
fset : Function to be used for setting an attribute value
fdel : Function to be used for deleting an attribute
doc : docstring

Now, the same program can be written using property type,

```
class rk:
	def __init__(self):
		self.value=0

	def fget(self):
		print("Get method")
		return self.value

	def fset(self, ty):
		print ("Set method")
		self.value = ty

	def fdel(self):
		print("delete method")
		del self.value       

	name = property(fget, fset, fdel, "I'm the property.")

r=rk()
r.name=1
print(r.name)
del r.name
Output

Set method
Get method
1
delete method
```

---
### Creating descriptors using property type and decorators

Python decorators are callable objects used to modify functions or classes. 

By using decorators we can modify the attribute methods.

Example to create descriptors using property type and decorators:
```
class rk(object):
	def __init__(self):
		self.i=0

	@property
	def inc(self):
		print("get method")
		return self.i

	@inc.setter
	def inc(self, ty):
		self.i=ty
		print ("Set method",self.i)

	@inc.deleter
	def inc(self):
		print ("delete method")
		del self.i

r=rk()

print(r.inc)
r.inc=3
del r.inc
Output

get method
0
Set method 3
delete method
```

---
###  Advantages of descriptors
Descriptors can increase the readability of a program 
- it can validate the data based on our requirements
- create a way to implement private variables and manage the data
- possible protect the attributes from any modifications and any updations

---
<!-- .slide: data-background="url('images/demo.jpg')" data-background-size="cover" --> 
<!-- .slide: class="lab" -->
## Demo time!
Descriptors

---
<!-- .slide: data-background="url('images/lab2.jpg')" data-background-size="cover"  --> 
<!-- .slide: class="lab" -->
## Lab time!
Descriptors