04:02:08
03:30:50 - file system
03:45:00 - ticktacktoe

# C

## libs

``` c
#include <stdio.h>
#include <stdlib.>
#include <stdbool.h>
```

## Comments

``` c
// this is a comment
/*
 this is a multi-line comment
*/
```

## Var Declarations

``` c
type <name> = <val>
```

## Data Types:

``` c
  char <var>                                                // %c | single character
  char <var>[size<int>]                                     // %s | array of characters, will cause buffer overflow if go beyong size<int>
  float <var> = 3.141592                                    // %f | 6-7 digits 4 bytes (32 bits of precision)
                  123456                                    
  double <var> = 3.141592653589793                          // %lf | 15-16 digits 8 bytes (64 bits of precision)
                   123456789012345                          
  bool <var> = true                                         // %d | 1 byte (true or false) shoud have #include <stdbool.h> in the header
  char <var> = 100                                          // %d or %c | 1 byte (-128 to +127)
  unsigned char <var> = 255                                 // %d or %c | byte (0 to +255) 
  short int <var> = 32767                                   // %d | 2 bytes (-32,768 to +32,767)
  unsigned short int <var> = 65535                          // %d | 2 bytes (0 to +65,535)
                                                            
  int <var> = 2147483647                                    // %d | 4 bytes (-2,147,483,647 to +2,147,483,647)
  unsigned int <var> = 4294967295L                          // %u | 4 bytes (0 to 4,294,967,295)
                                                            
  long long int <var> = 9223372036854775807                 // %lld | 8 bytes (-9Q to +9Q)
  unsigned long long int <var> = 184446744073709551615U     // %llu | 8 bytes (0 to 18Q)

  &<var>                                                    // %p | memory addreess
                                                            
  // 1D array                                               // sizeof(var1<array>) / sizeof(var1[0]) returns size of array
  type var[] = {val1, val2}                                 // array is fixed size
  type var[size<int>]                                       // if no val is init and size is uncertain
  var[index]                                                // access array by index
  var[index] = val                                          // mutate array value by index
                                                            
  // 2D array                                               // sizeof(var1<array>) / sizeof(var1[0]) returns the size of the rows
                                                            // sizeof(var1[0]) / sizeof(var1[0][0]) returns the size of the columns
  type var[][] = {{}}                                       // array is fixed size
  type var[size<int>][size<int>]                            // if no val is init and size is uncertain
  var[index][index]                                         // access array by indeces
  var[index][index] = val                                   // mutate array value by indeces
 
  // Array of Strings
  char <var>[][size<int>] = {}                              // sizeof(var1<array>) / sizeof(var1[0]) returns size of array    
  var[index]                                                // access array by index
  srtcpy(var[index], val<string>)                           // mutate array value by index                         
                                                            
  %.1                                                       // decimal precision
  %1                                                        // minimum field width
  %-                                                        // left align
                                                            
  const <type> <VAR>                                        // constant fixed value that cannot be altered by the program during its execution
  (<type>) var                                              // explicit type conversion or cast or casting
```

## Scape Operators:                                             

``` c
 \n                                                        // new line
 \t                                                        // tab
 \0                                                        // end line
 \<s>                                                      // print scape operators
```

## Bitwise Operators: - special operators used in bit level programming (knowing binary is important in this part) only works with integers

``` c
& - AND
| - OR
^ - XOR
<< - left shift
>> - right shift
~ - compliment
```
  
Examples:

``` c
int x = 6;  // 00000110
int y = 12; // 00001100
int z = 0;  // 00000000

x & y = 4   // 00000100
x | y = 14  // 00001110
x ^ y = 10  // 00001010
x << 1 = 12 // 00001100
x >> 1 = 3  // 00000011
~x = -7     // 11111001
```

## Memory:

memory: an array of bytes within RAM (street)\
memory block: a single unit (byte) within memory, used to hold some value (person)\
memory address: the address of where a memory block is located (house address)

### show memory addresses

```c
int a = 1;
printf("%d", sizeof(a)); = 4 - show byte size
printf("%p", &a); = 000000CE1C7FFD4C - show mem addreess
```

## Pointers:
``` c
*p - indirection operator

type *p<Name> = NULL - a good practice
p<Name> = &<varRef>
p<Name> - points to the mem addreess
*p<Name> - dereferencing, returns the value it is referecing from

// Pointer In Function
Sample(p<Name>);

type Sample(type *<name>){
  *<name> - deref
}
```

## Reserved Keywords:

``` c
sizeof(var)                                               // sizeof(var1<array>) / sizeof(var1[0]) returns the size of the array
```

## Basic Functions:

``` c
printf();                                                 // print a std
  ("%<t>" , valName);                                      
  ("%<t>p" , &valName);                                   // "&" reference an address in mem
scanf(string<formatSpecifier>, &<var>)                    // & is addreess
fgets(<var>, bufferSize<int>, stdin)                      // used for accepting input with whitespaces
```

## Switch Case:

``` c
switch(<var>){                                            
   case <matchVar>:                                        
      [block]                                              
      break;                                               
   case <matchVar>:                                        
      [block]                                              
      break;                                               
   default:                                                
      [block]                                               
}
```

## Math Functions:

``` c
#include <math.>                                          
double <var> = sqrt(<number>)                            // square root
double <var> = pow(base<number>, power<number>)          // power
int <var> = round(<float | double>)                      // round 
int <var> = ceil(<float | double>)                       // round up
int <var> = floor(<float | double>)                      // round down
double <var> = fabs(<number>)                            // absolute value
double <var> = log(<number>)                             // logarithm
double <var> = sin(<number>)                             //\
double <var> = cos(<number>)                             //| trigo
double <var> = tan(<number>)                             ///

```

## String Functions:

``` c
#include <string.h>
strlwr(<string>)                                         // converts a sting to lowercase
strupr(<string>)                                         // converts a string to uppercase
strcat(var1<string>, var2<string>)                       // appends var2 to end of var2
strncat(var1<string>, var2<string>, <int>)               // append n characters from var2 to var1 
strcpy(var1<string>, var2<string>)                       // copy var2 to var1
strncpy(var1<string>, var2<string>, <int>)               // copy n of characters of var2 to var1

strset(var1<string>, <string>)                           // sets all characters of a string to a given character
strnset(var1<string>, <string>, <int>)                   // sets first n characters of a string to a given character
strrev(var1<string>)                                     // reverse string
                                                          
strlen(var1<string>)                                     // returns string length as int
strcmp(var1<string>, var2<string>)                       // string compare all characters
strncmp(var1<string>, var2<string>, <int>)               // string compare n characters
strcmpi(var1<string>, var2<string>)                      // string compare all (ignore case);
strnicmp(var1<string>, var2<string>, <int>)              // string compare n characters (ignore case)
```
@Loops:

```c
//For:                                                      
  for(type <var1> = val; <var1> <= <var2>; <var1>++){     
    [block]                                                              
    return | break | bool                                 // end the loop              
  }                                                                     
//While:                                                    
  while(<condition>){                                     
    [block]                                                
    return | break | bool                                 // end the loop
  }                                                       
//Do-While:                                                 
  do{                                                     
    [block]                                                
    return | break | bool                                 // end the loop
  }while(<condition>)
```

@Function:

```c
type <func-name>(type <var>, type <var>){
  printf(<string>);                      
  return <var>;                                          // depends on the type
}                                        
<func-name>();                                           // invoke function         
```

### Function Prototypes:

``` c
type <func-name>(type <var>, type <var>);                // function without body
main()                                                   // main function                               
type <func-name>(type <var>, type <var>){                // function with body
  return <var>;                                      
}                                                    
```

## Data Structures:

### Enums

enum: enums are contants similar to TS enums

``` c
enum <name>{        // treated as integer e.g. associated integer by default or by explicity putting integers in dalcalration e.g. con1 = 1
  <constant1>, - 0
  <constant2>, - 1
  <constant3>, - 2
  <constant4>, - 3
  <constant5> - 4
}
enum <name> = <contant>                                   // returns an integer
if(<enum-name> == <constant-integer>)                     // returns true
if(<enum-name> == <constant-name>)                        // returns true
```

### Structs: - partially related to TS Interfaces

struct: is a custom data type which combines some data types as fields or properties

``` c
struct <var> {                              // Define a struct and this is a data type
type var1<field | property>;
type var2<field | property>;
  // Add more fields as needed
};

struct <struct-name> <var-name>;            // Declare a struct variable
struct <struct-name> <var-name> = {...};    // Initialize a struct variable

<var-name>.<field | property> = value1;     // Access struct fields
<var-name>-><field | property> = value2;
```
 
#### Notes:

1. Use structs to group related variables under a single name.
2. Structs help to create custom data types, making the code more modular and readable.
3. Access struct fields using the dot `.` operator.
4. Use `typedef` for shorthand declaration of struct types.
5. Memory layout is sequential for struct members.

#### Examples:

1. Basic Struct:

``` c
struct Point {
  int x;
  int y;
};

struct Point p1;
p1.x = 10;
p1.y = 20;
```

2. Array of Structs:

``` c
struct Point points[5];  // Array of 5 Point structs
```

3. Pointer to Struct:

``` c
struct Point *ptr = &p1;
    ptr->x = 30;  // Access via arrow operator
```
   

### Algo:

``` c
int main() { - bubble
int array[] = {7,3,6,10,8,5,1,9,4,2};             // sample array
int sizeOfArray = sizeof(array)/sizeof(array[0]); // returns size of array
int temp = 0;
for(int a=0; a<sizeOfArray; a++){   // holds the val to be swapped
  for(int b=0; b<sizeOfArray; b++){ // 
    if(array[a] > array[b]){
      temp = array[a];
      array[a] = array[b];
      array[b] = temp;
    }
  }
}
return 0;
}
```

## Shinanigans:

### Psuedo Random Numbers

```c
#include <stdio.h>
#include <stdlid.h>
#include <time.h>

int main(){
  srand(time(0));                       // use time to generate a seed
  int number1 = (rand() %  6)  +   1;   // rand() returns between 0 - 32,767
                         //max  //offset
  return 0;
}
```