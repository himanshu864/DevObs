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

- he function **`str()`** takes a value and converts it into a string. There are other functions such as **`int()`**, **`float()`** and **`bool()`**

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

> ****Syntax:**** enumerate(iterable, start=0)
> 
> ****Parameters:****
> 
> - ****Iterable:**** any object that supports iteration
> - ****Start:**** the index value from which the counter is to be started, by default it is 0
> 
> ****Return:**** Returns an iterator with index and element pairs from the original iterable

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

```python
def main():
    x = [x for x in range(5)] # [0,1,2,3,4]
    x = [x + 3 for x in range(5)] # [3,4,5,6,7]
    x = [x % 3 for x in range(5)] # [0,1,2,0,1]
    x = [x for x in range(2) for x in range(5)] # [0,1,2,3,4,0,1,2,3,4]
    x = [x for x in range(5) if x % 2 == 0] # [0,2,4]
```

