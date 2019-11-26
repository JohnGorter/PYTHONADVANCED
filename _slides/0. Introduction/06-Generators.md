# Iterators and Generators


---
### Iterators
Iterators are objects that can be iterated upon. 

Python iterator object must implement two special methods
- __iter__() 
- __next__()

They are collectively called the iterator protocol

An object is called iterable if we can get an iterator from it 
- most of built-in containers in Python like: list, tuple, string etc. are iterables
- the iter() function (which in turn calls the __iter__() method) returns an iterator from them
- use the next() function to manually iterate through all the items of an iterator

---
### Iterating Through an Iterator in Python
An elegant way of automatically iterating is by using the for loop. 

Using this, we can iterate over any object that can return an iterator, for example list, string, file etc.
```
>>> for element in my_list:
...     print(element)
...   
```

---
### How for loop actually works?
As we see in the above example, the for loop was able to iterate automatically through the list.

In fact the for loop can iterate over any iterable
```
for element in iterable:
    # do something with element
```
Is actually implemented as.
```
# create an iterator object from that iterable
iter_obj = iter(iterable)
# infinite loop
while True:
    try:
        # get the next item
        element = next(iter_obj)
        # do something with element
    except StopIteration:
        # if StopIteration is raised, break from loop
        break
```

So internally, the for loop creates an iterator object, iter_obj by calling iter() on the iterable

Ironically, this for loop is actually an infinite while loop.

---
### Building Your Own Iterator in Python
Building an iterator from scratch is easy in Python. 
We just have to implement the methods __iter__() and __next__().
- the __iter__() method returns the iterator object itself. If required, some initialization can be performed.
- the  __next__() method must return the next item in the sequence. On reaching the end, and in subsequent calls, it must raise StopIteration

---
### Python Infinite Iterators
It is not necessary that the item in an iterator object has to exhaust. 

There can be infinite iterators (which never ends). 

We must be careful when handling such iterator.

Here is a simple example to demonstrate infinite iterators.

The built-in function iter() can be called with two arguments 
- the first argument must be a callable object (function) 
- the second is the sentinel.

The iterator calls this function until the returned value is equal to the sentinel.

---
### Python Infinite Iterators Example
```
>>> int()
0
>>> inf = iter(int,1)
>>> next(inf)
0
>>> next(inf)
0
```

We can see that the int() function always returns 0. 
Passing it as iter(int,1) will return an iterator that calls int() until the returned value equals 1. 

This never happens and we get an infinite iterator


---
<!-- .slide: data-background="url('images/demo.jpg')" data-background-size="cover" --> 
<!-- .slide: class="lab" -->
## Demo time!
Iterators



---
### Generaotors
There is a lot of overhead in building an iterator in Python; 
- we have to implement a class with __iter__() and __next__() method
- keep track of internal states
- raise StopIteration when there was no values to be returned etc

This is both lengthy and counter intuitive. Generator comes into rescue in such situations.

---
### Generators (2) 
Python generators are a simple way of creating iterators. 

Simply speaking, a generator is a function that returns an object (iterator) which we can iterate over (one value at a time).

--- 
### How to create a generator in Python?
It is fairly simple to create a generator in Python. 

It is as easy as defining a normal function with yield statement instead of a return statement.

The yield statement pauses the function saving all its states and later continues from there on successive calls

---
### Differences between Generator function and a Normal function
- generator function contains one or more yield statement
    - when called, it returns an object (iterator) but does not start execution immediately
    - methods like __iter__() and __next__() are implemented automatically, so we can iterate through the items using next()
    - once the function yields, the function is paused and the control is transferred to the caller
    - local variables and their states are remembered between successive calls.
    - when the function terminates, StopIteration is raised automatically on further calls

---
### Generator example
Here is an example to illustrate all of the points stated above.

We have a generator function named my_gen() with several yield statements.

```
# A simple generator function
def my_gen():
    n = 1
    print('This is printed first')
    # Generator function contains yield statements
    yield n

    n += 1
    print('This is printed second')
    yield n

    n += 1
    print('This is printed at last')
    yield n
```

---
### Generator example output
```
>>> # It returns an object but does not start execution immediately.
>>> a = my_gen()
>>> # We can iterate through the items using next().
>>> next(a)
This is printed first
1
>>> # Once the function yields, the function is paused and the control is transferred to the caller.
>>> # Local variables and theirs states are remembered between successive calls.
>>> next(a)
This is printed second
2
>>> next(a)
This is printed at last
3
>>> # Finally, when the function terminates, StopIteration is raised automatically on further calls.
>>> next(a)
Traceback (most recent call last):
...
StopIteration
>>> next(a)
Traceback (most recent call last):
...
StopIteration
```

---
### Generator Remarks

- the value of variable n is remembered between each call
- unlike normal functions, the local variables are not destroyed when the function yields
- the generator object can be iterated only once.
- to restart the process we need to create another generator object using something like a = my_gen()

Note: One final thing to note is that we can use generators with for loops directly.
this is because, a for loop takes an iterator and iterates over it using next() function

```
# Using for loop
for item in my_gen():
    print(item)  
```

```
This is printed first
1
This is printed second
2
This is printed at last
3
```

---
### Python Generators with a Loop
Let's take an example of a generator that reverses a string.
```
def rev_str(my_str):
    length = len(my_str)
    for i in range(length - 1,-1,-1):
        yield my_str[i]

# For loop to reverse the string
# Output:
# o
# l
# l
# e
# h
for char in rev_str("hello"):
     print(char)
```

In this example, we use range() function to get the index in reverse order using the for loop

---
### Python Generator Expression
Simple generators can be easily created on the fly using generator expressions. 
- it makes building generators easy
- same as lambda function creates an anonymous function, generator expression creates an anonymous generator function
- the syntax for generator expression is similar to that of a list comprehension in Python but the square brackets are replaced with round parentheses

The major difference between a list comprehension and a generator expression is that 
- list comprehension produces the entire list
- generator expression produces one item at a time

They are kind of lazy, producing items only when asked for

---
### Python Generator Expression Example
```
# Initialize the list
my_list = [1, 3, 6, 10]

# square each term using list comprehension
# Output: [1, 9, 36, 100]
[x**2 for x in my_list]

# same thing can be done using generator expression
# Output: <generator object <genexpr> at 0x0000000002EBDAF8>
(x**2 for x in my_list)
```

We can see above that the generator expression did not produce the required result immediately
Instead, it returned a generator object with produces items on demand

---
### Python Generator Expression Example (2)
```
# Intialize the list
my_list = [1, 3, 6, 10]

a = (x**2 for x in my_list)
# Output: 1
print(next(a))

# Output: 9
print(next(a))

# Output: 36
print(next(a))

# Output: 100
print(next(a))

# Output: StopIteration
next(a)
```

---
### Python Generator Expression
Generator expression can be used inside functions. When used in such a way, the round parentheses can be dropped.
```
>>> sum(x**2 for x in my_list)
146
>>> max(x**2 for x in my_list)
100
```

---
### Why generators are used in Python?
There are several reasons which make generators an attractive implementation to go for.
- Easy to Implement
Generators can be implemented in a clear and concise way as compared to their iterator class counterpar
- Memory Efficient
A normal function to return a sequence will create the entire sequence in memory before returning the result
- Represent Infinite Stream
Generators are excellent medium to represent an infinite stream of data
Infinite streams cannot be stored in memory and since generators produce only one item at a time, it can represent infinite stream of data
- Pipelining Generators
Generators can be used to pipeline a series of operations. This is best illustrated using an example.

---
### Pipelining Generators
Suppose we have a log file from a famous fast food chain. 

The log file has a column (4th column) that keeps track of the number of pizza sold every hour and we want to sum it to find the total pizzas sold in 5 years

Assume everything is in string and numbers that are not available are marked as 'N/A'. A generator implementation of this could be as follows.
```
with open('sells.log') as file:
    pizza_col = (line[3] for line in file)
    per_hour = (int(x) for x in pizza_col if x != 'N/A')
    print("Total pizzas sold = ",sum(per_hour))
```

This pipelining is efficient and easy to read (and yes, a lot cooler!)

---
<!-- .slide: data-background="url('images/demo.jpg')" data-background-size="cover" --> 
<!-- .slide: class="lab" -->
## Demo time!
Generators

---
<!-- .slide: data-background="url('images/lab2.jpg')" data-background-size="cover"  --> 
<!-- .slide: class="lab" -->
## Lab time!
Iterators and Generators