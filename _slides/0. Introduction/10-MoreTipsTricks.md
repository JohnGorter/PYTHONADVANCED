# More Tips And Tricks

---
### In-Place Swapping Of Two Numbers.
```
x, y = 10, 20
print(x, y) 
x, y = y, x 
print(x, y) 
Output:
10 20
20 10
```

---
### Reversing a string in Python
```
a ="GeeksForGeeks"
print("Reverse is", a[::-1]) 
Output:
Reverse is skeeGroFskeeG
```

---
### Create a single string from all the elements in list
```
a = ["Geeks", "For", "Geeks"] 
print(" ".join(a)) 
Output:
Geeks For Geeks
```

---
### Chaining Of Comparison Operators
```
n = 10
result = 1 < n < 20
print(result) 
result = 1 > n <= 9
print(result) 
Output:
True
False
```

---
### Print The File Path Of Imported Modules
```
import os
import socket
  
print(os) 
print(socket) 
Output:
<module 'os' from '/usr/lib/python3.5/os.py'>
<module 'socket' from '/usr/lib/python3.5/socket.py'>
```

---
### Use Of Enums In Python
```
class MyName: 
    Geeks, For, Geeks = range(3) 
  
print(MyName.Geeks) 
print(MyName.For) 
print(MyName.Geeks) 
Output:
2
1
2
```

---
### Return Multiple Values From Functions
```
def x(): 
    return 1, 2, 3, 4

a, b, c, d = x() 
  
print(a, b, c, d) 
Output:
1 2 3 4
```

---
### Find The Most Frequent Value In A List
```
test = [1, 2, 3, 4, 2, 2, 3, 1, 4, 4, 4] 
print(max(set(test), key = test.count)) 
Output:
4
```

---
### Check The Memory Usage Of An Object
```
import sys 
x = 1
print(sys.getsizeof(x)) 
Output:
28
```

---
### Print string N times
```
n = 2; 
a ="GeeksforGeeks"; 
print(a * n); 
Output:
GeeksforGeeksGeeksforGeeks
```

---
### Checking if two words are anagrams
```
from collections import Counter 
def is_anagram(str1, str2): 
     return Counter(str1) == Counter(str2) 
print(is_anagram('geek', 'eegk')) 
  
print(is_anagram('geek', 'peek'))     
Output:
True
False
```

---
### THE ZEN OF PYTHON 
```
import this 
Output:

The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

---
###  Else with for/while loop 

It’s a special type of syntax that executes only if the for loop exits naturally, without any break statements.
```
def func(array): 
    for num in array: 
        if num%2==0: 
            print(num) 
            break # Case1: Break is called, so 'else' wouldn't be executed. 
    else: # Case 2: 'else' executed since break is not called 
        print("No call for Break. Else is executed")  
  
print("1st Case:") 
a = [2] 
func(a) 
print("2nd Case:") 
a = [1] 
func(a) 
Output:

1st Case:
2
2nd Case:
No call for Break. Else is executed
```

---
### Everything is by reference

Python doesn’t support pointers.

---
### Function Argument Unpacking 

Another awesome feature of Python. 
One can unpack a list or a dictionary as function arguments using * and ** respectively. 

This is commonly known as the Splat operator.
```
def point(x, y): 
    print(x,y) 
  
foo_list = (3, 4) 
bar_dict = {'y': 3, 'x': 2} 
  
point(*foo_list) # Unpacking Lists 
point(**bar_dict) # Unpacking Dictionaries 
Output:

3 4
2 3
```

---
### Indexers

Want to find the index inside a for loop? Wrap an iterable with ‘enumerate’ and it will yield the item along with its index. 
```
# Know the index faster 
vowels=['a','e','i','o','u'] 
for i, letter in enumerate(vowels): 
    print (i, letter) 
Output:
(0, 'a')
(1, 'e')
(2, 'i')
(3, 'o')
(4, 'u')
```

---
### Chaining

```
# Chaining Comparison Operators 
i = 5; 
  
ans = 1 < i < 10
print(ans) 
  
ans = 10 > i <= 9
print(ans) 
  
ans = 5 == i 
print(ans) 
Output:

True
True
True
```

---
### Infinities

We can’t define Infinities right? But wait! Not for Python. 

Example
```
# Positive Infinity 
p_infinity = float('Inf') 
  
if 99999999999999 > p_infinity: 
    print("The number is greater than Infinity!") 
else: 
    print("Infinity is greatest") 
  
# Negetive Infinity 
n_infinity = float('-Inf') 
if -99999999999999 < n_infinity: 
    print("The number is lesser than Negative Infinity!") 
else: 
    print("Negative Infinity is least") 
Output:

Infinity is greatest
Negative Infinity is least
```

---
### Comprehension
 
Instead of building a list with a loop, one can build it more concisely with a list comprehension. 

See this code for more understanding.
```
# Simple List Append 
a = [] 
for x in range(0,10): 
    a.append(x) 
print(a) 
  
# List Comprehension 
print([x for x in a]) 
Output:

[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---
### Slices

Finally, Python’s special Slice Operator,a way to get items from lists, as well as change them. 

See this code snippet
```
# Slice Operator 
a = [1,2,3,4,5] 
  
print(a[0:2]) # Choose elements [0-2), upper-bound noninclusive 
print(a[0:-1]) # Choose all but the last 
print(a[::-1]) # Reverse the list 
print(a[::2]) # Skip by 2 
print(a[::-2]) # Skip by -2 from the back 

Output:
[1, 2]
[1, 2, 3, 4]
[5, 4, 3, 2, 1]
[1, 3, 5]
[5, 3, 1]
```

