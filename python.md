# Python

## Contens

- [Operators](#op)
  - [Arithmethic](#op1)
  - [Logical Operators](#op2)
  - [Bitwise and Logical Operators](#op3)
  - [Identity Operators](#op4)
  - [Membership Operators](#op5)
- [Data Structures](#da)
  - [Lists](#dal1)
    - [List Comprehensions](#dal2)
    - [Built-In Functions](#dal3)
    - [2D List](#dal4)
  - [Tuples](#dat)
  - [Set](#das)
    - [Set Built-In Functions](#das1)
    - [Good for Membershipt Operators](#das2)
  - [Dictionaries](#dad)
- [Match Case](#mc)
- [Functions](#f)
  - [Default Params](#f1)
  - [Keywords Arguments](#f2)
  - [Arbitrary](#f3)
  - [*args](#f4)
  - [*kwargs](#f5)
  - [Mix *args and **kwargs](#f6)
- [Loops](#l)
  - [While](#l1)
  - [For](#l2)
  - [Loop in lists](#l3)
- [Modules](#m)
  - [Create Module](#m1)
- [OOP](#oop)
  - [Object](#oop1)
    - [Class](#oop11)
    - [Super()](#oop12)
    - [Instance()](#oop13)
    - [Class()](#oop14)
    - [Static()](#oop15)
  - [Inheritance](#oop2)
    - [Multiple Inheritance](#oop21)
    - [Multi-level Inheritance](#oop22)
  - [Polymorphism](#oop3)

import time -> has time related functions

## Time lib

``` python
time.sleep(int)  #pauses the system by secs
```

## **Comments**

``` python
# comment here
```

## **Conventions**

### Naming conventions

``` python
firstname_lastname = "var" #if two words

#printing
print("%D", var)
print(f" {var}") #string literals

#keywords
  type(var) # returns what type of data type `<class 'str'>`
  isinstance(i, dataType) # returns bool
  reversed(var) # reverses any iterable arrays

#casting 
var = int(var);
var = float(var);
var = str(var);
var = bool(var)

bool = True, False
string = ""
char = ''
```

## Strings Methods

**string is an object data type so it has a lots of methods**

``` python
len(strVar) # returns int
myString.rstrip() # removes any trailing whitespace (or specified characters) from the right end of a string
myString.split() # divides a string into a list of substrings based on a specified delimiter (separator)
myString.split(string<delimiter>, int<maxSplit>) # delimeters such as " ", "_", "-" that seperates word
```

### Access chars in string using index

``` python
var[int]
var[int<start>:int<end>:int<step>]
var[int<start>:int<end>]
var[:int<end>] # auto read start to end
var[int<start>:] # auto read from int<start> to end
var[::int<step>] # reads all but adds a step per read
 
#bonus
var[::-1] # read the string in reverse
# display strings multiple times
print(var * int)

```

## Input

``` python
var = input("String")
```


## <a id="op">Operators</a>

### <a id="op1">Arithmetic</a>

``` python
** # exponential
// # floor division
```

### <a id="op2">Logical Operators </a>

``` python
& , and # &&
| , or  # ||
! , not # !
```

### <a id="op3">Bitwise and Logical Operators</a>

``` python
& , and # &&
| , or  # ||
^ , xor # !(||)
~       # ! 
```

### <a id="op4">Identity Operators</a>

``` python
is     # ==
is not # !=
```

### <a id="op5">Membership Operators</a>

``` python
in      # this.obect is present in object
not in  # this.obect is not present in object
```

## <a id="da">Data Structures </a>

### <a id="dal1">Lists</a> -> Mutable, Ordered collections, more flexible

``` python
var = [1,2,3] # declaration
var[int]      # accessing
var[int]      # assigning

newVar = tuple(var) # used to create a list from an iterable object like a list or a string
# can convert tuple into list using list()
```

#### <a id="dal2">List Comprehensions</a>

``` python
var = [x * <int> for x in range(int<start>, int<end>)] # fill a list
var = [list.function() for list in lists]
var = [x for x in xs if x <operator> <int>]
var2 = [int(x) for x in myList] # converts all number in strings format into strings
```

#### <a id="dal3">Built-In Functions </a>

``` python
var.append(<var>)       # adds this value to the list
var.insert(<i>, <val>)  # adds val in the chosen index
var.remove(var)         # removes first occurance of the value
var.pop(index)          # removes a value by index
var.clear()             # clears the list
```

#### <a id="dal4">2D List </a>

``` python
var = [[1,2], [3,4]]
var[row][cols]
```

### <a id="dat">Tuples</a> -> Immutable, Ordered collections, faster

``` python
  var = (1,2,3,4)     # declaration
  # cause of Immutable nature, cant do assignments

  newVar = tuple(var) # used to create a tuple from an iterable object like a list or a string
  # can convert list into tuple using tuple()

  # tuple packing 
  var = 1, 2, 3
  # tuple unpacking   # basically destructuring in js
  x, y, z = var

  # concat two tuples
  var1 = (1,2,3)
  var2 = (4,5,6)
  var3 = var1 + var2 #-> 1,2,3,4,5,6
```

### <a id="das">Set</a> -> Mutable, Unordered collection (No duplicate elements)

``` python
var = {1,2,3,4} # declaration
# cannot use index notation because it is Unordered
```

#### <a id="das1">Set Built-In Functions</a>

``` python
var.add(var)
var.remove(var)
var.clear()
```

#### <a id="das2">Good for Membershipt Operators</a>

- is
- is not
- in
- not in

### <a id="dad">Dictionaries</a> -> A collection of {ket: value} pairs ordered and changable, No duplicates

``` python
var = { "one": 1, "two": 2, "three": 3}

dir(var)                 # view all key and values
help(var)                # in dept description
var.get(string<key>)     # get value using key, it not founc will return "None" as string
var.update({key: value}) # insert a key and value
var.update({key: value}) # change value of that matching key
var.pop(string<var>)  
var.popitem()            # removes the newest or last key-value pair that has been added
var.clear()              # clear all key->value
var.keys()               # gets all keys
var.values()             # gets all values

# print all key value using for loop
for key, value in var.items():
  #codeblock key, value  
```

## <a id="mc">Match Case</a> (switch case)

``` python
match var:
  case <val>:
    # code block 
    return
  case <val2> | <val3>:
    # code block 
    return
  case _:
    # code block 
    return
```

## <a id="f">Functions</a>

``` python
def <name>(param):
  return <val>
```
  
### <a id="f1">Default Params</a>

``` python
def <name>(param = val):
  return <val>
```

### <a id="f2">Keywords Arguments</a>

``` python
def <name>(param1, param2):
  
<name>(param1=val, param2=val) # any order of params by using keyword

# bonus
  end="" # place this string to the end
  sep="" # seperate params with this string
```

### <a id="f3">Arbitrary</a>

``` python
    *args     # allows you to pass multiple non-key arguments
    **kwargs  # allows you to pass multiple key-word arguments
    *         # unpack operator
```

#### <a id="f4">*args</a>

``` python
def name(*<name>):   # *<name> becomes a tuple
  # args can now be looped as it is a tuple
  
  name(1,2,3,4,5,6)  -> no error as it becomes a tuple
```

#### <a id="f5">*kwargs</a>

``` python
def name(**<name>):   # **<name> becomes a dictionary
  # args can now be looped as it is a dictionary

name(param1=1, param2=2, param3=3, param4=4)  # no error as it becomes a tuple
```

#### <a id="f6">Mix *args and **kwargs</a>
``` python
def name(*tuple,**dic): # if used, * should be before **
  # args can now be looped as it is a dictionary

name(1, 2, 3, 4, param1=1, param2=2, param3=3, param4=4)  # no error as it becomes a tuple
```

## <a id="l">Loops</a>

### <a id="l1">While</a>

``` python
    while <args>:
```

### <a id="l2">For</a> -> has 3 params

``` python
for <var> in rangle(args):
  # code block
for <var> in rangle(args<i, end, step>):
  # code block
```

#### <a id="l3">Loop in lists</a>

``` python
for <var> in <vars>:
  # code block for <var>
```

## <a id="m">Modules</a> -> use other code from other file

``` python
print(help("modules"))    # print the modules that are available

import <module>
import <module> as alias  # give module an alias
from <module> import functionName 

<module>.function()       # access module functions
```

### <a id="m1">Create Module</a>

``` python
#create file
#import file using import, no need ./
#then use the functions and variables from that module

# this should be at the end of that module/file 
if __name__ == "__main__": # doest run scripts when imported as module
# calls functions here when the script is called
```


## <a id="oop">OOP</a>

### <a id="oop1">Object</a> -> needs class to make many objects

#### <a id="oop11">Class</a> -> structs

``` python
class <Name>:             # self is similar to this. notation

  var = val               # class varliable, and is shared among these same instance
  counter = 0             # counsts how much instance of this object exist

  def __init__(self, params1, params2): # constructor method
    self.params1 = params1
    self.params2 = params2
    <Name>.counter+=1     # incremented whenever this class is instantiated

  //method                # self is required because of inheritance
  def <method_name>(self): 
    self.params1
  def <method_name>(self, paramsVal):
    self.params1 = paramsVal

var = <Name>(val1, val2);
print(var)                # prints mem address
print(var.params1)        # prints params1 val
print(<Name>.classVar)    # classes of intance class variables can be accessed directly 
```

##### <a id="oop12">Super()</a> method

``` python
class A:
  def __init__(self, name):
    self.name = name

  def fun1(self):
    print("hello");

class B(A):
  def __init__(self, name, number):
    super().__init__(name)
    self.number = number

  def this_class_func1(self):
    super().func1()
```

##### <a id="oop13">Instance()</a> method

``` python
# currently empty
```

##### <a id="oop14">Class()</a> method

``` python
# currently empty
```

##### <a id="oop15">Static()</a> method

``` python
# currently empty
```

#### <a id="oop2">Inheritance</a>

``` python
class Main:
  def __init__(self, name):
    self.name = name

  def action1(self):
    pass

  def action2(self):
    pass

class SubMain(Main):
  def action3(self):
    pass

class SubMain2(Main):
  pass
```

##### <a id="oop21">Multiple Inheritance</a>

``` python
class Main1:
  def __init__(self, name):
    self.name = name

class Main2:
  def __init__(self, name):
    self.name = name

class SuperMain(Main1, Main2):
  pass
```

##### <a id="oop22">Multi-level Inheritance</a>

``` python
class Base():
  def __init__(self, name):
    self.name = name

  def model(self):
    print("This is a building")

class Upper(Base):
  def definition(self):
    print("This is top of the base")

class Lower(Base):
  def definition(self):
    print("This is lower of the base")

top_building = Upper("Top");
lower_building = Lower("Top");

print(top_building.definition())    # This is top of the base
print(lower_building.definition())  # This is lwoer of the base

print(top_building.model())         # This is a building
print(lower_building.model())       # This is a building
```

#### <a id="oop3">Polymorphism</a>

``` python
# currently empty
```
