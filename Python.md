#dev #python

# Introduction
---
## Hello World
```python
def main():
    print("Hello World")

if __name__ == '__main__':
    main()
```

- No curly braces or closing semicolons
- Indentation necessary

- Automatic datatype
- Similar to javascript, formatted string literals and concatenation
## Input()
- By default, input function takes *strings*
```python
a = input('Enter a: ')
print('a = ', a)
print(f'a = {a}')
```

- Function **`str()`** takes a value and converts it into a string. There are other functions such as **`int()`**, **`float()`** and **`bool()`**

- ** - exponential.
- // - Floor Division
- Logical Operator : `and` `or` `not` instead of &&, ||, !
## elif:
```python
def main():
	a = 5
	b = 3
	a /= b # 1.66667
	if bool('True') == True and not(a == 1):
		print("Ya" + ("ta" * 3) + "!")
	else:
		print("nu uh")
# Yatatata!
```
- Optional bracket

**Pass**: Do nothing
**Continue**: move on to next iteration
**Break**: move out of the loop

- The clause *Try* attempts to execute a block of code and *except* executes another block of code if try fails. And *finally* runs regardless.

## Lambda Function
---

- Small, inline, anonymous function. Only one expression
```python
# Syntax
lambda [arguments]: [expression]
```

```python
# Example
sum = lambda a, b: a + b
greet = lambda name : f'hello, {name}'

def main():
    print(sum(3,5))
    print(greet("himanshu"))
```

- Higher-order functions are functions that can accept other functions, such as lambda functions, as arguments. Example: `map()`, `filter()`, and `sorted()`.

```python

def higher():
    nums = [1, 2, 3, 4, 5]

    # map()
    # returns a new list after applying given lambda function to each item in list
    squared = list(map(lambda a : a ** 2, nums))
    print(squared)

    # filter()
    # creates new list of elements for which given lambda function returns True
    odd = list(filter(lambda a : a % 2 == 0, nums))
    print(odd)

    # sorted()
    # uses lambda fns as keys for custom sorting
    rev = sorted(nums, key=lambda x : -x) # reverses nums
    print(rev)

    students = [('A', 18), ('B', 15), ('A', 12)]
    roll = sorted(students, key=lambda x : x[1]) # sorts based on i = 1
print(roll)
```

# Built- In Data Structures
---

## String
- Immutable
```python
def main():
    s = "My name is Himanshu!"
    print(s[0])
    print(s[3:7]) # slice - start index : end index + 1
    print(s[11:]) # from 11th index to end

# negative index to print letters from back
    print(s[-1]) # first from back
    print(s[-9:]) # 9th from back to end
    print(s[-9:-1]) # 9th from back to 2nd from back

    print(len(s)); # length

    print(s.upper()) # coverts all letters capital
    print(s.lower())
    print(s.title()) # Capitalize first letter of all words

    # split() : splits string into list of strings at argument
    print(s.split('name'))
```

## List - [ ]
- Mutable
- Faster insertion and deletion
```python
def listy():
    l = ['abc', 123, "v", 4.27, ['x', 4]] # flexible

    print(l[4][0])
    print(l[0:2]) # slicing works
    print(len(l)) # lengh

    l.append('hello') # appends argument to end
    print(l)

    l.remove(4.27) # removes 4.27
    print(l)

    l.pop(1) # pops 1st index
    print(l)
```

## Tuples - ( )
- Immutable
- More memory and time efficient than list
- Faster index accessing
```python
def tuply():
    t = ('abc', 34, 'd', -4, 5.5, (3,7,4))
    print(t)
    print(t[0]) # indexing works
    print(t[1:3]) # slicing works
    print(len(t)) # length
    print(max(t[5])) # returns max when tuple of same data type

    tp = ('abc', 'a', 'b', 'acb', 'a')
    print(min(tp))
    print(sorted(tp))

    print(tp.index('a')) # returns index of first occ. of arg.
    print(tp.count('a')) # returns freq. of arg.
```

## Dictionaries - { }
- Key-value pairs
- keys must be immutable. Eg: strings, tuples, numbers, etc
- values can be mutable. Eg: lists, nests dictionaries.
- No indices or slicing here
- Can access, update and add new element using keys
```python
def dict():
    d = {
        'h' : 'himanshu',
        2 : [3,2,'a'],
        ('x', 'y') : {6 : 9}
    }
    print(d['h']) # access
    d['h'] = 'aggarwal' # update
    d[2].append(0) # modify value
    d[3] = 5 # add new
    print(len(d))
```

- *update()*: adds arg. dictionary. updating existing keys and adding new
```python
    dp = {'a' : 3, 2 : 5}
    d.update(dp)
```

- *.keys()* and *.values()* can be used to return the list of keys and values of a dictionary.
```python
    print(d.keys())
    print(d.values())
```

- use *del* keyword to delete any key-value pair
```python
	del d['h']
```

## Sets - { }
A set is an immutable, unordered collection of unique elements that can consist of integers, floats, strings and tuples.

```python
def sets():
    s1 = {'himanshu', 2, 234.2, 'b', 2}
    print(s1)

    # set() create set from list removing duplicates
    lst = ['a', 'b', 3, 3]
    s2 = set(lst)
    print(s2)

    # use in to check if value exists
    print('himanshu' in s1)
    print('himanshu' in s2)

    # immutable but can add unique elements
    s2.add('c')
    # removes existing element from set
    s1.remove('himanshu')
    print(s1)
```

```python
    # union() joins iterable object with existing object
    print(s1.union(s2))
    print(s1) # Note: s1 doesn't update

    # update() take any iterable object
    # (tuple, lists, dictionaries, sets)
    # and adds object to existing set
    # s1.update(lst)
    s1.update(s2)
    print(s1)
```

```python
    # set is iteratable hence for loop
    for x in s2:
        print(x)
```

# Misc
---
- use `end=''` inside print() to customise output's other than default `'\n'`

```python
def main():
    print("h", end='')
    print("ello", end=' ')
    print("bro", end='!\n')
    print("himanshu")

# output:
	# hello bro!
	# himanshu
```

### range()
	range() takes three arguments: (start, stop, step)
	if enter only one argument -> (stop) ; start = 0; step = 1
	if enter two arguments -> (start, stop) ; step = 1
- again, don't count stop.
Example:
```python
def main():
    for i in range(5, 0, -1):
        print(i, end=' ')
    print()
# 5, 4, 3, 2, 1
```

### Enumerate

> **Syntax:** enumerate(iterable, start=0)
> 
> **Parameters:**
> 
> - **Iterable:** any object that supports iteration
> - **Start:** the index value from which the counter is to be started, by default it is 0
> 
> **Return:** Returns an iterator with index and element pairs from the original iterable

Example:
```python
def main():
    num = [5,3,1,2,4]
    for i, element in enumerate(num):
        print(i, element)
```

### \*args and \*\*kwargs
To spread arguments when printing or as inputs. basically spread operator for list and dictionaries respectively.

### Slice Operator
again [start:stop:step] similar to *for* loops
- [:2:] -> from start, and before 2nd index
- [4:2:-1] -> 4th index, 3rd index
- [::-1] -> reverses the object

## Comprehension

> Read in reverse

Syntax:
```python
[expression for variable in iterable if condition]
```

> **Parameters**
> 
> - **`expression`**: What you want in your new list (e.g., `x`, `x+3`, `x%3`).
> - **`for variable in iterable`**: Loops over the sequence (`range(5)` is like a for loop iterating from 0 to 4).
> - **`if condition`** _(optional)_: Filters elements based on the condition (e.g., `x % 2 == 0`).

```python
def main():
    x = [x for x in range(5)] # [0,1,2,3,4]
    x = [x + 3 for x in range(5)] # [3,4,5,6,7]
    x = [x % 3 for x in range(5)] # [0,1,2,0,1]
    x = [x for x in range(2) for x in range(5)] # [0,1,2,3,4,0,1,2,3,4]
    x = [y for y in range(2) for x in range(5)] # [0,0,0,0,0,1,1,1,1,1]
    x = [x for x in range(5) if x % 2 == 0] # [0,2,4]
```

**Example 4** in c++:

`for x in range(5)` means 0, 1, 2, 3, 4
`for x in range(2) for ...` means nested for loops, i.e. twice range(5)
`[x for x in ...]` means return actual list twice. i.e. actual value
`[y for y in ...]` implies returning list of iterations i.e. i in case of nested loops in c++

```cpp
vector<int> x;
for (int i = 0; i < 2; ++i)
    for (int j = 0; j < 5; ++j)
        x.push_back(j);
```

# Let Us Python
---

# Unit 1
---

- High level programming language
- Free, quality, productivity, portability, libraries, integration, joy
- Powerful, Automatic, Ready-made stuff, Easy
- Dynamic Typing (check errors at runtime)

## Uses
- System Programming
- Building GUI
- Internet Scripting
- Game programming
- Scientific programming
- Robotics
- Database programming
- Component Integration (can invoke c++, frameworks, etc )
- Machine Learning
- Google (Web Search System), Youtube (Video Sharing), Movie animation

### **Paradigms**
Style of structuring and coding
One program may use many paradigms

#### Procedural
- Implements one statement at a time
- Uses functions but treats them like statements (instruction for computer)
- sequential - step by step
- *Imperative* : how're u finna do it? `amma go there, and punch him 3 times`

#### Functional
- Decompose problem into set of functions (taking input, returning output)
- mathematical equations like expression (code that produces a value)
- *Declarative* : what're u finna do? `amma beat his ass`

#### Object-Oriented
- like real world, creating mini-world of objects
- in college, objects are professors, students, staff, papers, courses, etc
- Each Object has a state (values) and behaviour (interface / methods), from the class that created it.
- Objects call each other's interface

#### Event-driven
- used for programming GUI applications containing elements (window, buttons, etc)
- interact with elements, and emit messages via listener methods
- Asynchronous

# Unit 2
---

## Compiler vs Interpreter
**Compiler** is a software that converts your entire code into machine code for the computer to process.

**Interpreter**, on the other hand, is already binary.

Eg: `$ python hello.py`

Here python is the interpreter that will be stored in the memory and has two components
- Compiler
- Python Virtual Machine

Compiler will convert `hello.py` into *Byte Code*

These Byte code, can't be understood by the processor. But instead will be processed by the *Python Virtual Machine*.

So that's how everything works on the hardware

CPython is written in C. (official, popular) - python3
There's also Jython, in java
PyPy - in RPython
IronPython - in C#

**IDE**
- NetBeans, PyCharm, VSCode

**PyPI** : Python Package Index. For installing pre-built third party packages.

Some packages that are popular for Data Science:
- **NumPy**: Advanced Mathematical Operations - multi-dimen. arrays
- **SciPy**: Scientific Computing Library - image processing, optimizing
- **Panda**: Library for manipulating numeric tables and time series
- **MatPlotLib**: 2D and 3D Data visualization
- **OpenCV**: Open Source Computer Vision

**pip**: tool for installing packages from PyPI

More tools for python
- **Jupyter Notebook**: flexible browser based interactive tool
- **Google Colab**: Jupyter env to run code on google cloud
- **Spyder**: Scientific Python Development Environment

##### Python Programming Modes
- *Interactive mode:* explore syntax, help and debug small: shell
- *Script mode:* proper programming: \*.py

# Unit 3
---

- Case sensitive language
- identifier used to name a variable, function, class, module, or other objects
- Python has 33 keywords. All lowercase except *True* and *False*

### Python Types
- Basic Types: int, float, complex, bool, string, bytes : (no char datatype)
- Container Types: list, tuple, set, dict
- User-Defined Types: class

### Basic Types
- **int** - binary 0b, decimal 12, hexadecimal 0x, etc
- **float** - fractional or exponential
- **complex** - 3 + 2j
- **bool** - True and False
- **string** - immutable characters between ' ', " " or "" ""
- **byte** - binary data

> Use **type()** function to check data type of a value

- int's have *arbitrary precision value*. Hence, no overflow
- same with float. In approximate binary representation

No need to define type of variable. Python understands from context during execution. Hence, dynamically typed.

#### Multiple Variable Assignment
```python
a = 10; b = 20; c = "Himanshu" # use ; as statement separator
d, e = 8, 9
x = y = z = 5
```

### Arithmetic Operators
- `/` - performs true division and returns float
- `//` - performs floor on division and returns integer
- `%` - remainder
- `**` - exponential

#### Operation Nuances
```python
print(10 // 3)  # 3
print(-10 // 3) # -4. Since division is -3.33 and floor is -4
```

> **`a % b`** is evaluated as `a - (b * (a // b))`

```python
print(4 % 3)   #  1
print(-4 % 3)  #  2
print(4 % -3)  # -2
print(-4 % -3) # -1
```

```python
print(True + True)  # 2
print(True * False) # 3
```

### Precedence and Associativity

![[Screenshot 2024-12-03 at 7.09.17 PM.png]]

When tie between operators of same *precedence*. Settled using *associativity*

Eg: multiplication and division same precedence. Hence solve left to right
```python
x = 3 * 4 / 5  # (3 * 4) / 5 = 2.4
y = 3 / 5 * 4  # (3 / 5) * 4 = 2.4
```

### Type Conversion

- operation between int and float will yield float
- int and complex -> complex
- float and complex -> complex

```python
int("23") # 23
int(3.33) # 3
int(-3.33) # -3
chr(86) # V
ord("E") # 69
```

> use **`ord()`** function return ascii value of one character string

### Build-in Functions
```python
abs(x)
pow(x, y)
min(a, b, c, ...)
max(a, b, c, ...)
round(x, [,n]) # returns x rounded on n digits after .
bin(10) # returns binary equivalent of 10. i.e. 0b1010
```

### Build-in Modules

- **math**: useful mathematics functions

```python
import math

def main():
    print(math.sqrt(10)) # 3.16...

# maths
pi, e  # values of constants pie and e
sqrt(x)
factorial(x)
log(x) # base e
log10(x)
exp(x) # e raised to x
ceil(x)
floor(x)

# trigonometry
degrees(x)
sin(x)
cos(x)
tan(x)
```

- **cmath**: performing operations of complex numbers functions

- **random**: random number generation functions

```python
import random

def main():
    print(random.random()) # random number between 0 and 1
	print(random.randint(10, 15)) # random between range (included)
```

- **decimal**: precise arithmetic operations functions

### Python Type Jargon

- **Collection**: a generic term for container types
- **Iterable**: collection that can be iterated over using loop
- **Ordered collection**: elements are stored in same order as insertion. Hence, indexing.
- **Unordered collection**: order not preserved. can't predict. Hence, no indexing
- **Sequence**: ordered collection
- **Immutable**: unchangeable collection
- **Mutable**: changeable collection

```
String - "" - ordered collection, immutable, iterable
List - [] - ordered collection, mutable, iterable
Tuple - () - ordered collection, immutable, iterable
Set - {} unordered collection, mutable, iterable
Dict - {} - unordered collection, keys immutable, value immutable, iterable
```

> start with \# for one line comments
> type between `'''...'''` or `"""..."""` for multi-line comments
> Indentation matters in python
 
**print spaces:**
```python
print('''
hello
		asd
''')
```

**String Literals**:
```python
x = "himanshu"
print(f'hello, {x}')
```

**Multi-lining**
- long statements can be written in multiple lines by ending each line expect last with `\`
- multi-line statements within `[], {}, or ()` don't need `\`
```python
total = maths + toc + \
		english + sst + \
		civics + pe

days = ["1asdf", "as",
		"adf"]
```

## Classes and Objects

- In Python, every type is a class. So `int, float, complex, bool, str, list, tuple, set, dict` are all ready made classes.

- ***Class*** is a blueprint for creating objects.
- It defines attributes (variables) and methods (functions) that it's object will have.

```python
class MyClass:
    def __init__(self, name):  # Constructor
        self.name = name      # Instance attribute

    def greet(self):          # Instance method
        return f"Hello, {self.name}!"
```

- ***Object*** is an instances of a class.
- It has its own copy of attributes and can call methods defined in the class.

```python
obj = Myclass("Himanshu")

print(obj.name) # attribute
print(obj.greet()) # call methods
```

- **`__init__` Method**:
    - The class constructor.
    - Automatically called when an object is created.
    - Used to initialize object attributes.
- **`self`**:
    - Refers to the current instance of the class.
    - Must be the first parameter of instance methods.
- **Class vs Instance**:
    - **Class Attributes**: Shared by all instances.
    - **Instance Attributes**: Unique to each object.