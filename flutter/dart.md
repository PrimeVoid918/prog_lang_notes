## Reference

[https://www.youtube.com/watch?v=CzRQ9mnmh44](https://www.youtube.com/watch?v=CzRQ9mnmh44)
timestamps: [timestamps.md](timestamp.md)
(03:27:36) -> currently at

## Variables

```dart
//<datatype> <variableName> = <value>

int firstVal = 12;
double doubleVal = 12;


bool nameVal = true;

// same as any in typescript
dynamic someValue = 123

// string is an object wrapper same as java that has built in methods
String nameVal = "sample";

// Use only when the value must change.
var variable = 12

// Dart replacement for JS const.
// runtime values (including async results)
final variable = 12

// Flutter default when possible.
// static / compile-time values
const variable = 12

// optional variable
int? someVar = null

```

## Printing

``` dart
print(" hello ${ expression }")
```

## Statements

```dart

if (expression){

}else if{

}else {

}

final name = user.name ?? null;
final raceType = user.isHuman ? "Human" : "Unclassified";

switch(someValue){
   case var x when ['apple', 'orange', 'banana'].contains(x):
   // this is special of swtich statement for pattern matching
    print('Fruit!');
    break;
  case "sample2":
    print("Sample2 here");
    break;
  default:
    print("nothing was selected");
    break;
}

// relation operators
when
is //type checking
is!

```

## Looping

```dart
for(init; condition; increment/decrement){
  codeblock
}

while(argument){
  // codeblock
}

do {
  // codeblock
}while(argument)

```

## Function

``` dart
<datatype> fnName(params){

}

// when calling it,
fnName; // refers to the function itself - Closure
fnName(); // calls the function and executes it

// has type `dynamic` by default
fnName(){

}

(int, String) getUserInfo(int age, String name) {
  return (age, name);
}
final userInfo = getUserInfo(12, "helbard");
print(userInfo.$1); // integer age

final (age, name) = getUserInfo(12, "helbard"); // destructuring way
print(age, name);

// named arguments
///-------------------------------
(String firstPositionalArgument, {String name, int? age}) printName (String firstPositionalArgument, {required String name, int? age}){
  return (firstPositionalArgument: firstPositionalArgument, name: name, age: age)
}
final printTheName = printName("say", {name: "jom"})

// Definition
void printName(String pos, {required String name, int? age}) {
  print("$pos $name is $age");
}

// Call (Correct)
printName("Hello", name: "Jom", age: 25);
///-------------------------------

// return a function
//Function printSomething(){
//  return () {
//    print("sample")
//  }
//}
void Function() getPrinter() {
 return () => print("Sample"); 
}
final someThing = printSomething()
print(something())

// EEFIE
(){
// codeblock
}()

// Arrow function
String someStuff => "say?";
```
