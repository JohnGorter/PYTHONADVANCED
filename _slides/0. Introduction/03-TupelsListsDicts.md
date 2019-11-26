# Tupels, Lists, Sets and Dictionaries

---
### Introduction
Lists - a list of values
- each one of them is numbered, starting from zero 
- you can remove values from the list, and add new values to the end

Tuples 
- are just like lists, but you can't change their values
- the values that you give it first up, are the values that you are stuck with for the rest of the program
- each value is numbered starting from zero, for easy reference. 

---
### Introduction (2)

Sets
- a collection which is unordered and unindexed
- sets cannot have multiple occurrences of the same element
- it makes sets highly useful to efficiently remove duplicate values from a list or tuple 

Dictionaries 
- in a dictionary, you have an 'index' of words (key), and for each of them a definition (value)
- the values in a dictionary aren't numbered 
- the values aren't in any specific order, either 
- you can add, remove, and modify the values in dictionaries

---
### Tuples
Tuples are pretty easy to make: 
- give your tuple a name and the list of values it will carry

```
months = ('January','February','March','April','May','June',\
'July','August','September','October','November','  December')
```

---
### Lists
Lists are extremely similar to tuples
- but are modifiable (or 'mutable', as a programmer may say), so their values can be changed. 

Most of the time we use lists, not tuples, because we want to easily change the values of things if we need to

---
### Lists (2)
Lists are defined very similarly to tuples. 
```
cats = ['Tom', 'Snappy', 'Kitty', 'Jessie', 'Chester']
```

note the square brackets, not parentheses

You recall values from lists exactly the same as you do with tuples. For example, to print the name of your 3rd cat you would do this:

```
print cats[2]
print cats[0:2]
```


---
### Lists (3)
Lists can be modified
- use the 'append()' function
```
cats.append('Catherine')
del cats[1]
```


---
### Dictionaries
```
#Make the phone book:
phonebook = {'Andrew Parson':8806336, \
'Emily Everett':6784346, 'Peter Power':7658344, \
'Lewis Lame':1122345}
```

```
#Add the person 'Gingerbread Man' to the phonebook:
phonebook['Gingerbread Man'] = 1234567
```

```
del phonebook['Andrew Parson']
```


---
### Dictionaries (2)
```
#A few examples of a dictionary

#First we define the dictionary
#it will have nothing in it this time
ages = {}

#Add a couple of names to the dictionary
ages['Sue'] = 23
ages['Peter'] = 19
ages['Andrew'] = 78
ages['Karren'] = 45

#Use the function has_key() - 
#This function takes this form:
#function_name.has_key(key-name)
#It returns TRUE
#if the dictionary has key-name in it
#but returns FALSE if it doesn't.
#Remember - this is how 'if' statements work -
#they run if something is true
#and they don't when something is false.
if ages.has_key('Sue'):
    print "Sue is in the dictionary. She is", \
ages['Sue'], "years old"

else:
    print "Sue is not in the dictionary"

#Use the function keys() - 
#This function returns a list
#of all the names of the keys.
#E.g.
print "The following people are in the dictionary:"
print ages.keys()

#You could use this function to
#put all the key names in a list:
keys = ages.keys()

#You can also get a list
#of all the values in a dictionary.
#You use the values() function:
print "People are aged the following:", \
ages.values()

#Put it in a list:
values = ages.values()

#You can sort lists, with the sort() function
#It will sort all values in a list
#alphabetically, numerically, etc...
#You can't sort dictionaries - 
#they are in no particular order
print keys
keys.sort()
print keys

print values
values.sort()
print values

#You can find the number of entries
#with the len() function:
print "The dictionary has", \
len(ages), "entries in it"
```


---
### Sets
Sets are a mutable collection of distinct (unique) immutable values that are unordered

You can initialize an empty set by using set()
```
emptySet = set()
```

To intialize a set with values, you can pass in a list to set().
```
dataScientist = set(['Python', 'R', 'SQL', 'Git', 'Tableau', 'SAS'])
dataEngineer = set(['Python', 'Java', 'Scala', 'Git', 'SQL', 'Hadoop'])
```


Sets containing values can also be initialized by using curly braces.
```
dataScientist = {'Python', 'R', 'SQL', 'Git', 'Tableau', 'SAS'}
dataEngineer = {'Python', 'Java', 'Scala', 'Git', 'SQL', 'Hadoop'}
```

---
### Add and Remove Values from Sets
To add or remove values from a set, you first have to initialize a set.
```
# Initialize set with values
graphicDesigner = {'InDesign', 'Photoshop', 'Acrobat', 'Premiere', 'Bridge'}
```
Add Values to a Set
```
graphicDesigner.add('Illustrator')
```

---
### Remove Values from a Set
There are a couple ways to remove a value from a set.
```
graphicDesigner.remove('Illustrator')
```

The drawback of this method is that if you try to remove a value that is not in your set, you will get a KeyError.

```
graphicDesigner.discard('Premiere')
```
```
graphicDesigner.pop()
```

It is important to note that the method raises a KeyError if the set is empty.

---
### Remove All Values from a Set
You can use the clear method to remove all values from a set.
```
graphicDesigner.clear()
```

---
### Iterate through a Set
Like many standard python data types, it is possible to iterate through a set.
```
# Initialize a set
dataScientist = {'Python', 'R', 'SQL', 'Git', 'Tableau', 'SAS'}

for skill in dataScientist:
    print(skill)
```

If you look at the output of printing each of the values in dataScientist, notice that the values printed in the set are not in the order they were added in. 

This is because sets are unordered.

---
### Transform Set into Ordered Values
This tutorial has emphasized that sets are unordered. If you find that you need to get the values from your set in an ordered form, you can use the sorted function which outputs a list that is ordered.

The code below outputs the values in the set dataScientist in descending alphabetical order (Z-A in this case).
```
sorted(dataScientist, reverse = True)
```

---
### Remove Duplicates from a List
Sets are the fastest way to remove duplicates from a list. To show this, let's study the performance difference between two approaches.

Approach 1: Use a set to remove duplicates from a list.
```
print(list(set([1, 2, 3, 1, 7])))
```

Approach 2: Use a list comprehension to remove duplicates from a list (If you would like a refresher on list comprehensions, see this tutorial).
```
def remove_duplicates(original):
    unique = []
    [unique.append(n) for n in original if n not in unique]
    return(unique)

print(remove_duplicates([1, 2, 3, 1, 7]))
```

using sets to remove duplicates is more efficient

---
### Set Operation Methods
A common use of sets in Python is computing standard math operations such as 
- union:  the set of all values that are values of A, or B, or both
- intersection: the set of all values that are values of both A and B
- difference: the set of all values of A that are not values of B
- symmetric difference: the set of all values that are values of exactly one of two sets, but not both


---
<!-- .slide: data-background="url('images/demo.jpg')" data-background-size="cover" --> 
<!-- .slide: class="lab" -->
## Demo time!
Using Lists, Tupels, Sets and Dictionaries

---
<!-- .slide: data-background="url('images/lab2.jpg')" data-background-size="cover"  --> 
<!-- .slide: class="lab" -->
## Lab time!
Using Lists, Tupels, Sets and Dictionaries



