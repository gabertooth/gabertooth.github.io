---
layout: post
title:      "In Depth Look into linspace, map, lambda, and enumerate"
date:       2019-04-21 11:55:20 -0400
permalink:  in_depth_look_into_linspace_map_lambda_and_enumerate
---


This blog post will go over a few Python methods that have not been covered in the curriculum thus far.  The following methods will be explored with example code provided: linspace, map, lambda, and enumerate methods. 

**1. Linspace:  Linspace is a numpy object that returns evenly spaced numbers over a specified interval. Below is the layout with the arguements of linspace.**

numpy.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)

a. start/stop: The number you would like to start/end the interval at.

b. num= 50: Number of samples to generate. Default is 50. Must be non-negative.

c. endpoint=True/False: If True, stop is the last sample. Otherwise, it is not included. Default is True.

d. retstep= True/False: If True, (samples, steps) where steps is the interval spacing between samples

e. dtype=None: the data type you would like your array to output in, if not specified defaults to the original data type

**Example: **

np.linspace(0, 5, num=5, endpoint=True, retstep= True, dtype= None)

**Example Output: **

(array([0. , 1.25, 2.5 , 3.75, 5 ]), 1.25)

**2. Map: map() function returns a list of the results after applying the given function to each item of a given iterable (list, tuple etc.)**

map(fun, iter): 

a. Fun (function): It is a function to which map passes each element of given iterable.
b. Iter (Iterable): It is a iterable which is to be mapped

**Example: **

def addition(n):
      return n + n
numbers = (0, 5, 10, 15) 
result = map(addition, numbers) 
print(list(result))

**Example Output: **

{0,10,20,30}

Essentialy this method allows you to apply a specified function across a list of iterables and is very useful when dealing with a process that is repeatable and tedious.  This allows you to do it all in one tail swoop. 

**3. Lambda: A lambda function is a small anonymous function created by a user. A lambda function can take an unlimited number of arguments(x, y, z, etc.), but can only have one expression. **

lambda arguments : expression

**Example: **

1. x = lambda a : a + 10
    print(x(5))

2. x = lambda a, b : a * b
     print(x(5, 6))

**Example Output:**

1. 15
2. 30

The power of lambda is better shown when you use it as an anonymous function inside another function. Creating a function inside a function essentially. 

We can also combine lambda functions with map functions, example provided below:

**Example:**

li = [5, 7, 22, 97, 54, 62, 77, 23, 73, 61] 
finallist = list(map(lambda x: x*2 , li)) 
print(finallist)

**Example Output: **

[10, 14, 44, 194, 108, 124, 154, 46, 146, 122]

**4. Enumerate: Enumerate allows you to add a counter to an iterable and returns it n a form of a enumerate object. This enumerate object can then be used directly in for loops or be converted into a list of tuples using list() method.**

**Example:**

Ex_1=['Philly', 'D.C.', 'NYC']

Obj_1=enumerate(Ex_1)

list(Obj_1)

**Example Output: **

[(0, 'Philly'), (1, 'D.C.'), (2, 'NYC')]












