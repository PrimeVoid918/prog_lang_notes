02:51:00

# C++

## Makefile defaults

use Makefile for easier compilation

``` makefile
g++ -Wall -std=c++17 -o index index.cpp
```

## Libs

``` c
#include <iostream>
#include <ctime>    // for randoms
#include <iostream> // input output
```

## ?

``` c++
::    // scope resolution operator
```

## std

``` c++
std::cout << <string> - standard (std) character out (cout) << output
<< std::endl - standard (std) endline (endl)  // will flush output buffer

std::cin >> <var>                             // will read string but stops at whitespace
std::getLine(std::cin, <var>)                 // reads the full string along with whitespacesa and stop at endline
std::getLine(std::cin >> std::ws, <var>)      // ws will eliminate any \n or whitespaces

//printing with string literal, << is similar to js `+`
std::cout << "String " << <var>
```

### String functions

``` c++
var.lenth()                         // returns the lenth  
var.empty()                         // returns a bool value
var.clear()                         // clears the string
var.append(var)                     // appends the string on this string
var.at(index)                       // returns a character in that index
var.insert(index, <var>)            // insert this string to that particular index in this string
var.fint(val)                       // gives the index position of that it finds
var.erase(startIndex, endIndex)     // erases a portion of a string
```

## Standard Math Functions

```c++
#include <cmath>
std::max(<var1>, <var2>)            // returns the greater of all values
std::min(<var1>, <var2>)            // returns the minimum of all values
std::pow(<var1>, <var2>)            // raises the power 
std::sqrt(<var1>)                   // returns the square
std::abs(<var1>)                    // returns the absolute val
std::round(<var1>)                  // returns the round
std::ceil(<var1>)                   // returns the round up
std::floor(<var1>)                  // returns the round down
```

## Built in functions

``` c++
fill(start, end, val)
```

## Types

### Type Conversion

```c++
type <var> = (type) val             // casts the value
std::cout << (char) 100             // 100 integer is casted into char printing an ascii value instead
  
const <type> <VAR> 

int <var>
double <var> 
char <var>
bool <var>                          // true or false | 1 or 0

// string is an object that represents a sequence of text
std::string <var>
```

### Types In Pointers

``` c++
//Null val = 
nullptr                           // keyword represents a null pointer literal
                                    //nullptrs are helpful when determining if an address was successfully assigned to a pointer 
// good practice 
type *pointer = nullptr
```

## Namespace

``` c++
namespace <var>{
int sample = 2;
}
main{
// using namespace <var> - main now reads all variable that is under this namespace and <var> namespace prefix in print is not neccesary
std::cout << <var>::sample;
}

//shortcut for shorter syntax inside main func
using std::cout;
using std::string;

string <var> = "sample";
cout << "sample" << <var>;
```

### Varibale Scope

``` c++
//global
int num = 2;
//function
int main(){
int num = 3       // redeclaration dont cause an error because it reads this as local variable
// ::num - to use the global variable
}
```

## Data Structures

## TypeDef: - in TS it is similar to Type Aliases

``` c++
typedef <type> <newTypeName_t>  // creates a new name for that type e.g /typedef char[15] FiftenChar
typedef struct {...<fields | properties} <var>;
// leaverage the use of word structs and other types keyword into use the name of the typedef
// c++ new | instead of `typedef`, use `using` because it is more suitable for templates
using <newTypeName_t> = <type>
```

### Array

``` c++
type <var>[] = {};

// get addresses by index
&array[index]
(array + index)
```

## Loops

### For Each

``` c++
for(type var : <dataset>){ - data set e.g. arrays

}
```

## Functions

``` c++
//some of the basics are from C
 
//parts of functions
name(params)                  // function signitures

//pass functions by reference - modifies the values permanently of that referenced variable
function (type &<var>){}      // changes the value of the passed variable that is being referenced
// pass reference using Pointers
function (type *<var>){
  cont sample = 0
  sample = *<var>             // usses * to reference the value
}
function (&<var>);            // use & to reference this variable to this function in this method, e.g. pointer * method
```

### Pass array to function

``` c++
function(type var[], type size){}   // var decays into a pointer and getting the size becomes unavailable
function(array)                     // just normal passing like a variable
```

### Function overload

``` c++
//same function name but diffferent paramater/number of parameters, the compile will determin what function to use by the number of arguments
//different type in parameter is considered
//different return types are not considered
main{
  sample();
  sample2(name);
  sample3(name, age);
}
```

### Function templates - basically TS Generic Topic

``` c++
// decribe what a function looks like, can be used for function overload
template <typename T, typename U>     // `template` and `typename` is a keyword and T and U is a type Aliases
T <name>(T x, U y){
  // now it can recieve 2 data types,
}
// another 
template <>
type add<type, type>(type x, type y) {
  return x + " " + y;  // Adds a space when concatenating strings
}
```

## Shinanigans

### Generate Random Numbers

``` c++
std::random_device rd;
std::mt19937 gen(rd());
std::uniform_int_distribution<int> dist(0, SIZE);
int random = dist(gen);
dist(gen)                   // generate number on call
```

## Memory

#### Dynamic Mem

``` c++
<ptr> = new type  // use `new` to allocate mem in the heap rather than the stack
delete <ptr>      // free up the mem
delete[] <ptr>    // if the pointer is an array
```  

## OOP

``` c++
int name                      // attributes
function()                    // methods

class <Name>{
protected:                    //-
  type var                    //-| protected field - public field can access protedted field when inhereted in child, but not outside
                              //-/
private:                      //-
  type var;                   //-| private field - cannot be accessed by outside and child
                              //-/
public:                       //-
  type var;                   //-| public field
                              //-/

//Constructor
<Name>(                       //arguments| type <paramVar>){
  this->objectVar = paramVar;
  objectVar = paramVar;       // if attribute name differ from param name;
}
//Overloaded constructors - same as function overloading
//setter
  type set<Name>(params){     // often void is the return type
    this-><attr> = params
  }
//getter
  type get<Name>(){
    return this-><attr>
  }
```

 private | public - Inheritance Types
 *Inheritance
  class <Object2> : <inheritanceType> <Object2>{

  }
 *Composition

@Shinanigans
 *Aggregate Initialization
  StructType{value1, value2}
   Vector2 vel = {0, 0};
   Vector2 vel{5, -3};
   funct(Vector2{5, -3})
  