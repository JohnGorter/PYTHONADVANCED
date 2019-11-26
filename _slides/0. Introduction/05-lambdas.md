# Lambdas

---
### What is Lambda?
Lambdas, also known as anonymous functions, are small, restricted functions which do not need a name (i.e., an identifier). 

Lambda functions were first introduced to the field of mathematics by Alonzo Church in the 1930s.

Today, many modern programming languages like Java, Python, C#, and C++ support lambda functions to add functionality to the languages.

In Python, lambda expressions (or lambda forms) are utilized to construct anonymous functions

---
### Lambdas in Python

Every anonymous function you define in Python will have 3 essential parts:
- The lambda keyword
- The parameters (or bound variables)
- The function body

A lambda function can have any number of parameters, but the function body can only contain one expression

Moreover, a lambda is written in a single line of code and can also be invoked immediately

---
### Syntax 
The formal syntax to write a lambda function is as given below:
```
lambda p1, p2: expression 
```

Here, p1 and p2 are the parameters which are passed to the lambda function

However, notice that we do not use brackets around the parameters as we do with regular functions

---
### Examples
Example 1
```
adder = lambda x, y: x + y
print (adder (1, 2))
```

Example 2
```
# What a lambda returns
string='some kind of a useless lambda'
print(lambda string : print(string))
Output:
<function <lambda> at 0x00000185C3BF81E0>
```
the lambda itself returns a function object

In this example, the lambda is not being called by the print function but simply returning the function object 

Example 3
```
# What a lambda returns #2
x="some kind of a useless lambda"
(lambda x : print(x))(x)

Output:
some kind of a useless lambda
```

Now, the lambda is being called, and the string we pass gets printed at the console. But what is that weird syntax, and why is the lambda definition covered in brackets? Let's understand that now.

---
### Using lambdas with Python built-ins
Lambda functions provide an elegant and powerful way to perform operations using built-in methods in Python. 

It is possible because lambdas can be invoked immediately and passed as an argument to these functions.

IIFE in Python Lambda
```
(lambda x: x + x)(2) 
```

```
sequences = [10,2,8,7,5,4,3,11,0, 1]
filtered_result = filter (lambda x: x > 4, sequences) 
print(list(filtered_result))
```

```
sequences = [10,2,8,7,5,4,3,11,0, 1]
filtered_result = map (lambda x: x*x, sequences) 
print(list(filtered_result))
```

```
from functools import reduce
sequences = [1,2,3,4,5]
product = reduce (lambda x, y: x*y, sequences)
print(product)
```

---
### When should you not use Lambda?
You should never write complicated lambda functions in a production environment. 

It will be very difficult for coders who maintain your code to decrypt it. 

If you find yourself making complex one-liner expressions, it would be a much superior practice to define a proper function. As a best practice, you need to remember that simple code is always better than complex code

---
### Lambdas vs. Regular functions
As previously stated, lambdas are just functions which do not have an identifier bound to them. 

In simpler words, they are functions with no names (hence, anonymous). 

- Lambda functions can only have one expression in their body.
- Regular functions can have multiple expressions and statements in their body.
- Lambdas do not have a name associated with them.
- Regular functions must have a name and signature.
- Lambdas do not contain a return statement because the body is automatically returned
-  Functions which need to return value should include a return statement.


---
<!-- .slide: data-background="url('images/demo.jpg')" data-background-size="cover" --> 
<!-- .slide: class="lab" -->
## Demo time!
Lambdas

---
<!-- .slide: data-background="url('images/lab2.jpg')" data-background-size="cover"  --> 
<!-- .slide: class="lab" -->
## Lab time!
Lambdas