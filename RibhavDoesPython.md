Python is a high level programming language created by Guido van Rossum - fondly known as Benevolent Dicatator of Life.

- can invoke C, C++ libraries and java components.
- can communicate with frameworks such as COM, .NET.
- With appropriate glue code, Python can subclass C++, java, C#.

Features
-

- Dynamic Typing,
- No Variable Declaration,
- Automatic allocation and Garbage Collection,
- Supports classes, modules and exceptions.
- permits componentization and reuse,
- powerful containers - Lists, Dictionaries, Tuples, etc.

## Programming Paradigms
- Paradigm means organization principle. It is also known as model.
- Programming paradigm/model is a style of building the structure and elements of computer program.
- There exist many programmig models like functional, procedural, object-oriented, Event-driven, etc.

#### Functional Programming Model.

1. Functional programming decomposes a problem into a set of functions. These functions provide the main source of logic in the program.
2. Functions take input parameters and produce outputs. Python provides functional programming techniques like lamda, map, reduce and filter.
3. In this model, computation is treated as evaluation of mathematical functions.

#### Procedural Programming Model.
- Procedural Programming solves the problem by implementing one statement at a time. Thus it contains steps that are executed in a specific order.
- It also uses functions, but these are not mathematical functions like one used in functional programming. Functional programming focuses on expressions, whereas Procedural Programming focuses on statements.
- The statements dont have values and instead modify the state of some conceptual machine.

#### Object-oriented programming Model
- This model mimics the real world by creating inside the computer a mini-world of objects.
- In a University system objects can be VC, Professors, Non-teaching staff, students, courses, semesters, examinations, etc.
- Each objects has a state (values) and behaviour (interface/methods). Objects get state based on the class from which it created.

#### Events-driven Programming Model
- This model is popularly used for programming GUI applications containing elements like windows, check boxes, buttons, combo boxes, scroll bars, menus, etc.
- When we interact with these elements (like clicking a button, moving the scrollbar, or selecting a menu item) events occur and these elements emit messages. There are listner methods that are registered with these GUI elements which react to these events.

#### Third-party Packages
- Pythonists in Python communnity create packages and make it available for use for other programmers. They use PyPi- Python Package Index.
  1. NumPy: Advanced mathematical operations library with support for large multi-dimensional arrays and matrices.
  2. SciPy: Scientific computing library for optimization, integration, interpolation, signal processing, image processing, etc.
  3. Pandas: Library for manipulating numerical tables and time series.
  4. MatPlotLib: 2D and 3D Data visualization library.
  5. OpenCv: Open source Computer vision library.


```python
import sys #to determine version of python installed in system
print(sys.version)

import keyword  # makes the module 'keyword' available
print(keyword.kwlist)
```

```python
print(0.1+0.2)
```

    0.30000000000000004



```python
# operation a%b is evaluated as a-(b*(a//b)). This can be best understood using the following examples
print(3%10)
print(3%-10)
print(-3%10)
print(-3%-10) 
```

    3
    -7
    7
    -3


#### Conversions
- Mixed mode operations:
     1. operation between int and float will yield float.
     2. operation between int and complex will yield complex.
     3. operation between float and complex will yield complex.

#### Built-in Modules
- math - many useful mathematics functions.
- cmath - functions for performing operations on complex numbers.
- random - functions related to random numbers generations.
- decimal - functions for performing precise operations.


```python
import math 
import random 
print(math.factorial(5))
print(math.degrees(math.pi))
print(random.random())
print(dir(__builtins__))
print(dir(math))
```

    120
    180.0
    0.9849124238923627
    ['Arithme...

#### Classes and Objects
- In Python every type is a class. So int, float, complex, bool, str, list, tuple, set, dict are all classes. These are ready-made classes. Python also permits us to create user-defined classes
- An object is created from a class. A class describes two things- the form an object created from it will takes and the methods that can be used to access and manipulate the object 


```python
a = 30 
b = 'Good'
print(a, b)
print(type(a), type(b))
print(id(a), id(b))
print(isinstance(a, int), isinstance(b, str)) #prints True True

a = 3
b = 3
print(id(a), id(b))
print(a is b)
a = 30
print(id(a))
```

    30 Good
    <class 'int'> <class 'str'>
    140715882114392 2109665402992
    True True
    140715882113528 140715882113528
    True
    140715882114392


# Strings

### What are Strings?
- Python string is a collection of Unicode characters.
- if there are characters like ' " or \ within a string, they can be retained in two ways:
    1. escape them by preceding them with a \\.
    2. prepend the string with a 'r' indicating that it is a raw string.
- Examples of positive and negative indexing:


```python
msg = 'Hello'
print(msg[0])
print(msg[4])
print(msg[-0])
print(msg[-1])
print(msg[-2])
print(msg[-5])
```

    H
    o
    H
    o
    l
    H



```python
msg = 'Rafting'
print(msg[3:100]) 
#print(msg[100]) error since 100th element doesn't exist
```

    ting


	### String Properties
- Python strings are immutable-they cannot be changed.
- strings can be concatenated using +.
- string can be replicated during printing. ()
- whether one string is part of another can be found out using in.
- Different categories of string methods are given below.
    *  content test function
    1. isalpha() - checks if all characters in string are alphabets.
    2. isdigit() - checks if all characters in string are digits.
    3. isalnum() - checks if all characters in string are alphabets or digit.
    4. islower()
    5. startswith()
    6. endswith()

    *  search and replace
    1. find() - searches for a value, return its position.
    2. replace() - replace one value with another.

    *  trim whitespace
    1. lstrip() - removes spaces from the left.
    2. rstrip() - removes spaces from the right.
    3. strip() - removes whitespaces from the left and right.


```python
print('-'*50) #prints 50 dashes
print('e' in 'Hello') #prints True

msg = 'Surreal'
print(len(msg))
print(min(msg))
print(max(msg))
print(type(msg))
print(id(msg))
print(msg.partition('r'))
print(msg.split('u'))
print(msg.upper())
print(msg)
print("-".join(msg))
```

    --------------------------------------------------
    True
    7
    S
    u
    <class 'str'>
    2056580460688
    ('Su', 'r', 'real')
    ['S', 'rreal']
    SURREAL
    Surreal
    S-u-r-r-e-a-l



```python
lst = ['desert', 'dessert', 'to', 'too', 'lose', 'loose']
for i, ele in enumerate(lst):
    print(i, ele)
```

    0 desert
    1 dessert
    2 to
    3 too
    4 lose
    5 loose


# Console Input/Output
# receive full name
name = input('Enter full name')
\# separate first name, middle name and surname
fname, mname, sname = input('Enter full name:').split()
print(name)
print(fname)
print(mname)
print(sname)
n1, n2, n3 = [int(n) for n in input('Enter three values:').split()]
print(n1+10, n2+20, n3+30)

numbers = [int(n) for n in input("Enter the numbers with space:").split()]
for nn in numbers:
    print(nn)
### Console Output
- Build-in function print() is used to send output to screen.
- print(objects, sep='', end='\n', file = sys.stdout,flush = False)<br>
This means that by default objects will be printed on screen(sys.stdout), separated by space(sep = '') and last printed object will be followed by a newline (end ='\n'). flush = False indicates that output stream will not be flushed.
- There are 4 ways to control the formatting of output:
    1. Using formatted string literals - easier
    2. Using the format() method - older.
    3. C printf() style - legacy
    4. Using slicing and concatenation operation - difficult<br>

    Today (1) is most dominantly used method followed by (b).


```python
# Using formatted string literals (often called fstrings):
r, l, b = 1.5678, 10.5, 12.66
print(f'radius= {r}')
print(f'length = {l} breadth = {b} radius = {r}')

name = 'Sushant Ajay Raje'
for n in name.split():
    print(f'{n:1}')

```

    radius= 1.5678
    length = 10.5 breadth = 12.66 radius = 1.5678
    Sushant
    Ajay
    Raje



```python
# Using format() method of string object:

r,l,b = 1.5678, 10.5, 12.66
name, age, salary = 'Rakshita', 30, 53000.55

# print in order by position of variables using empty{}
print('name = {} age = {} salary {}'.format(name, age, salary))

# print in any desired order 
print('age= {1} salary={2} name={0}'.format(name, age, salary))

# print name in 15 columns, salary in 10 columns
print('name = {0:8} salary = {1:9}'.format(name, salary))
```

    name = Rakshita age = 30 salary 53000.55
    age= 30 salary=53000.55 name=Rakshita
    name = Rakshita salary =  53000.55


# Lists
- Container is an entity which contains multiple data items. it is also known as a collection or a compound data type.
- A list can grow or shrink during execution of the program. hence it is also known as a dynamic array. Beacause of this nature of lists they are commonly used for handling variable length data.


```python
animal = ['Zebra', 155.55, 110]
ages = [25,26,25,27,26]
num = [10]*5
lst=[]

print(animal[1], ages[3])

print(animal[1:3])
print(ages[3:])
```

    155.55 27
    [155.55, 110]
    [27, 26]



```python
# Looping in lists 
animals = ['Zebra', 'Tiger','Lion','jackal', 'Kangaroo']
# using while loop
i = 0
while i < len(animals):
    print(animals[i])
    i += 1
# using for loop more convenient
for a in animals:
    print(a)

for index, a in enumerate(animals):
    print(index, a)
```

    Zebra
    Tiger
    Lion
    jackal
    Kangaroo
    Zebra
    Tiger
    Lion
    jackal
    Kangaroo
    0 Zebra
    1 Tiger
    2 Lion
    3 jackal
    4 Kangaroo



```python
# Concatenation 
lst = [12,25,34,345,54]
lst += [44,55,66]
print(lst)

# Merging
s = [10,20,30]
t = [100,200,300]
z = s+t
print(z)

#Conversion
l = list('Africa')
print(l)


```

    [12, 25, 34, 345, 54, 44, 55, 66]
    [10, 20, 30, 100, 200, 300]
    ['A', 'f', 'r', 'i', 'c', 'a']


- Aliasing - On assigning one list to another, both refer to same list. Changing one changes other. This assignment is known as shallow copy or aliasing.
- Cloning - This involves copying of one list to another. After copying both refer to different lists. This operation is known as deep copy


```python
# we can check if a list is empty using not operator.
lst = []
if not lst:
    print('Empty List')
```

    Empty List



```python
# Using Built-in Functions on Lists
lst = [10,20,30,40,50]
del(lst[3]) 
print(lst)
del(lst[2:5]) #delete items 2 to 4 from the list
print(lst)
del(lst[:]) # delete entire list
lst=[] # another way to delete entire list

# if multiple variable are referring to same lists then deleting one doesn't delete others
```

    [10, 20, 30, 50]
    [10, 20]



```python
# List Mehtods 
lst = [12, 25,13,23,22,16,17]
lst.append(22)
print(lst)
lst.remove(13)
print(lst)
#lst.remove(30) reports value error30 is absent in list
print(lst.pop(3))
lst.insert(3, 21)
print(lst.count(23)) # return the no. of times
#ldx= lst.index(50) reports value error30 is absent in list
```

    [12, 25, 13, 23, 22, 16, 17, 22]
    [12, 25, 23, 22, 16, 17, 22]
    22
    1



```python
# unpacking a string
s = 'Hello'
l = [*s]
print(l)
ite
# unpacking a list
x = [1, 2, 3, 4]
y = [10, 20, *x, 30]
print(y)
```

    ['H', 'e', 'l', 'l', 'o']
    [10, 20, 1, 2, 3, 4, 30]


# Tuples
- Though a list can store dissimilar data, it is commonly used for storing similar data.
- though a tuple can store similar data it is commonly used for storing dissimilar data. The tuple data is enclosed within () as shown below.


```python
a = () # empty tuple
b = (10,) # tuple with one item., after 10 is necessary
c = ('Sanjay', 25, 34555.60) # tuple with dissimilar items
d = (10, 20, 30, 40)

# while initializing a tuple we can drop ()
c = 'Sanjay', 25, 34555.50  #tuple with multiple items
print(type(c)) # c is of the type tuple

# items in a tuple can be repeated, i.e tuple may contain duplicate items. However, unlike list, tuple elements cannot be repeated usig a*.
tpl1 = (10,)*5
print(tpl1)
tpl2 = (10)*5
print(tpl2)
print(type(tpl2))
```

    <class 'tuple'>
    (10, 10, 10, 10, 10)
    50
    <class 'int'>



```python
# Like string and list, tuple too can be sliced to yield smaller tuples.
emp = ('Sanjay', 23, 23000, 1760, 2040)
print(emp[1:3])  #prints (23, 23000)
print(emp[3:]) 
```

    (23, 23000)
    (1760, 2040)


- Looping is similar to Lists, we can also use enumerate

## Basic Tuple Operations
- Mutability: Unlike list, a tuple is immutable, ie it cannot be modified.
- Since a tuple is immutable operations like append, remove and insert do not work with a tuple.
- Though a tuple itself is immutable, it can contain mutable objects like lists.
- if a tuple contains a list, the list can be modified since list it is a mutable object.



```python
t1 = (1,2,3)
t2 = (1,2,3)
t3 = t1
print(t1 is t2)
print(t1 is t3)
```

    False
    True


### Tuple Methods


```python
tpl = (12,15,13,23,22)
print(tpl.count(23))
print(tpl.index(22))
```

    1
    4
    [23, 22, 15, 13, 12]



```python
import operator
tpl = (['Priyanka',24,3455.50],['aailesh',25,4555.50])
print(sorted(tpl))
print(sorted(tpl, key=operator.itemgetter(2)))
```

    [['Priyanka', 24, 3455.5], ['aailesh', 25, 4555.5]]
    [['Priyanka', 24, 3455.5], ['aailesh', 25, 4555.5]]


# Sets
- Sets are  like lists, with an exception that they do not contain duplicate entries.
- while storing an element in a set, its hash value is computed using a hashing technique to determine where it should be stored in the set.
- since hash value of an element will be same, no matter in which order we insert the elements in a set, they get stored in the same order.
- it is possible to create a set of strings and tuples, but not a set of lists. Since strings and tuples are immutable, their hash value remains same at all times, Hence a strings or tuples is permitted. However, a list may change, so its hash value may change, hence a set of lists is not permitted.
- Being an unordered collection, items in a set cannot be accessed using indices.
- Sets cannot be sliced using [].


```python
s = {12,15,13,23,22,16,17}
for ele in s:
    print(ele)
```

    16
    17
    22
    23
    12
    13
    15



```python
# Sets are mutable
s = {'gate', 'fate', 'late'}
s.add('rate')
print(s)

# for immutable set
s = frozenset({'gate', 'fate', 'late'})
#s.add('rate') error
```

    {'rate', 'late', 'gate', 'fate'}


- Concatenation - doesn't work
- Merging - doesnt work
- Conversion - works
- Aliasing - works
- cloning - works
- Searching - works
- Identity - works
- Comparison - works
- Emptiness - works
- Two Sets cannot be concatenated using +.
- Two sets cannot be merger using the form z = s+t.
- 


```python
s = {12, 15, 13, 23, 22, 16, 17}
t = {13, 15, 22}
print(s.issuperset(t))
print(s.issubset(t))
print(s.isdisjoint(t))
```

    True
    False
    False



```python
# mathematical Set  Operations

# sets
engineers = {'Vijay', 'Sanjay', 'Ajay', 'Sujay', 'Dinesh'}
managers = {'Aditya', 'Sanjay'}

# union - all people in both categories
print(engineers | managers)

# intersection = who are engineers and managers
print(engineers & managers)

# difference - engineers who are not managers
print(managers-engineers)

# difference - managers who are not engineers
print(managers- engineers)


```

    {'Sanjay', 'Dinesh', 'Aditya', 'Ajay', 'Sujay', 'Vijay'}
    {'Sanjay'}
    {'Aditya'}
    {'Aditya'}


# Dictionaries
- Dictionary is a collection of key - value pairs.
- The Dictionary also as maps or assiciative arrays.
- A dictionary contains comma separated key: value pairs enclosed within
- Dictionary cannot be sliced using[].


```python
d1 = {} # empty dictionsarly
d2 = {'A101': 'Amol', 'A102': 'Anil', 'B103': 'Ravi'}

# Different keys may have same value.
d = {10: 'A', 20: 'A', 30 : 'Z'}

print(d)
print(d[10])
```

    {10: 'A', 20: 'A', 30: 'Z'}
    A



```python
courses = {'DAA': 'CA', 'AOA': 'ME', 'SVY': 'CE'}

# iterate over key-value pairs
for k, v in courses.items():
    print(k,v)

for k in courses:
    print(k)

for v in courses.values():
    print(v)

for i,(k,v) in enumerate(courses.items()):
    print(i, k, v)
```

    DAA CA
    AOA ME
    SVY CE
    DAA
    AOA
    SVY
    CA
    ME
    CE
    0 DAA CA
    1 AOA ME
    2 SVY CE



```python
courses = {'CS101': 'CPP', 'CS102': 'DS', 'CS201': 'OOP'}
for k,v in reversed(courses.items()):
    print(k,v)
```

    CS201 OOP
    CS102 DS
    CS101 CPP



```python
c = {'CS101':'CPP', 'CS102': 'DS', 'CS201':'OOP'}
d = {'ME126':'HPE', 'ME102': 'TOM', 'ME234': 'AEM'}

print(c.get('CS102', 'ABSENT'))
print(c.get('EE102', 'ABSENT'))

c.update(d)
print(c.popitem())
print(c.pop('CS102'))
c.clear()
print(c)
```

    DS
    ABSENT
    ('ME234', 'AEM')
    DS
    {}



```python
c = {'CS101':'CPP', 'CS102': 'DS', 'CS201':'OOP'}
d = {'ME126':'HPE', 'ME102': 'TOM', 'ME234': 'AEM'}

combined = {**c, **d}
print(combined)
```

    {'CS101': 'CPP', 'CS102': 'DS', 'CS201': 'OOP', 'ME126': 'HPE', 'ME102': 'TOM', 'ME234': 'AEM'}


# Comprehension


```python
import random

# generate 20 random numbers in the range 10 to 100
a = [random.randint(10, 100) for n in range(20)]
print(a)

# generate square and cube of all numbers between 0 and 10
a = [(x, x**2, x**3) for x in range(10)]
print(a)

a = [(x, x**2, x**10) for x in range(10)]
print(a)

# generate a list of even numbers in range 10 to 30
a = [2*n for n in range(5,16)]
print(a)

# from a list delete all numbers having value betweeen 20 and 50
a = [num for num in a if num<=20 and num>=10]
print(a)
```

# Functions




```python
# variable-length argument
def print_it(*args):
    print()
    for var in args:
        print(var, end=' ')

print_it(10)
print_it(10, 3.14, 'Sicilian')
print_it(10, 3.14, 'Sicilain')
```

    
    10 
    10 3.14 Sicilian 
    10 3.14 Sicilain 


```python
def print_it(**kwargs):
    print()
    for name, value in kwargs.items():
        print(name, value, end=' ')

print_it(a = 10)
print_it(a = 10, b = 3.14)
print_it(a = 10, b = 3.14, s = 'Sicilian')
dct = {'Student' : 'Ajay', 'Age':23}
print_it(**dct)
```

    
    a 10 
    a 10 b 3.14 
    a 10 b 3.14 s Sicilian 
    Student Ajay Age 23 

- if a function is to receive required as well as optional arguments then they must occur in following order :
    1. postional argument
    2. variable- length argument
    3. keword arguments
    4. variable-length keyword argument
- while defining a function default value can be given to arguments. Default value will be used if we do  not pass the value for that argument during the call.


```python
# Suppose a function is expecting keyword arguments and the arguments to be passed are in a dictionary . In sucn a case we need to unpack the dictionary using  ** opertor before passing it to the function
def print_it(name = 'Sanjay', marks = 75):
    print(name, marks)

d = {'name': 'Anil', 'marks': 50}
print_it(*d)
print_it(**d)
```

    name marks
    Anil 50


# Recursion

- The case when a recursive call is made is called the recursive call, whereas the other case is called the base case.
- A simple program that calculates factorial of a given number using a recursive function is given below, followed by a brief explanation of its working.


```python
def refact(n):
    if n==0:
        return 1
    else:
        p = n * refact(n-1)
    return p

num = int(input('Enter any number: '))
fact = refact(num)
print('Factorial value =', fact)
```

    Enter any number:  5


    Factorial value = 120


- if we are to define a function which generates and returns a list of lists containing all possible combination of numbers 1,2 and 3 we can do so through following program:


```python
def generate(n):
    lol = [i for i in range(n**n)]
    pos = 0
    for i in range(1, n+1):
        for j in range(1, n+1):
            for k in range(1, n+1):
                t = [i, j, k]
                lol[pos] = t
                pos += 1
    return lol

l = generate(3)
print(l)
```

	    [[1, 1, 1], [1, 1, 2], [1, 1, 3], [1, 2, 1], [1, 2, 2], [1, 2, 3], [1, 3, 1], [1, 3, 2], [1, 3, 3], [2, 1, 1], [2, 1, 2], [2, 1, 3], [2, 2, 1], [2, 2, 2], [2, 2, 3], [2, 3, 1], [2, 3, 2], [2, 3, 3], [3, 1, 1], [3, 1, 2], [3, 1, 3], [3, 2, 1], [3, 2, 2], [3, 2, 3], [3, 3, 1], [3, 3, 2], [3, 3, 3]]


- if we are to generate all possible combinations of 1,2,3,4 the we will have to introduce one more for loop. if genrate() is to remain generic we cannot dunamically add this loop.
- We can make generate() function create the desired combination by using recursion in place of loops as shown in the following program:


```python
def generate(n):
    t = []
    lol = [[] for i in range(n**n)]
    helper(n,t,lol)
    return(lol)

def helper(n, t, lol):
    global j
    if len(t) == n:
        lol[j] = lol[j] + t
        j += 1
        return 
    for i in range(1, n+1):
        t.append(i)
        helper(n, t, lol);
        t.pop()

j = 0
l = generate(3)
print(l)
```
