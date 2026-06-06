(03:27:36)


(00:00:00) Course Overview
(00:02:16) What is Dart?
(00:03:52) Dart SDK
(00:06:57) Print Statement
(00:09:59) Operators
(00:14:39) Comments
(00:17:31) Variables
(01:11:35) Control Flow
(01:37:52) Exercise 1
(01:46:06) Loops
(02:10:49) Functions
(02:46:53) Classes !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
(03:41:10) Inheritance
(03:59:58) implements keyword
(04:10:13) Abstract Classes
(04:15:03) Object Oriented Programming (OOP) in Dart
(04:17:09) Polymorphism
(04:20:52) Abstraction
(04:23:12) Encapsulation
(04:25:11) OOP Brief
(04:26:14) Mixins
(04:33:40) Class Modifiers
(04:40:48) Lists
(05:23:04) Sets
(05:25:39) Maps
(05:50:32) Enums
(06:03:03) Exception Handling
(06:11:45) Futures
(06:56:08) Streams
(07:19:46) (Bonus) Creating Records
(07:23:57) (Bonus) Patterns & Pattern Matching
(07:36:11) Extensions
(07:42:25) Introduction to Flutter
(07:42:35) Installing Flutter
(07:51:59) Installing Android Studio & Configuring for Android
(07:56:37) Installing Xcode & Configuring for iOS
(07:58:47) Installing VS Code
(08:00:24) Exploring VS Code
(08:04:41) Creating & Exploring The Flutter Project
(08:18:27) Running Flutter App
(08:31:11) Writing First Flutter Code!
(08:32:34) Importing Packages and material.dart
(08:35:20) runApp function in Flutter
(08:37:24) What are Widgets?
(08:38:10) Text Widget
(08:55:24) Types of Widgets
(08:57:22) What is State?
(08:58:48) Stateless Widget
(09:11:43) Material & Cupertino Design
(09:13:51) MaterialApp
(09:17:45) Scaffold Widget
(09:21:37) Center Widget
(09:26:28) Widget Tree
(09:29:09) Splitting & Extracting Widgets
(09:34:49) What is BuildContext?
(09:37:38) Importing Files & Magic of Flutter Extension
(09:40:05) Relative Importing
(09:42:47) Breaking Down The Currency Converter App
(09:43:31) Column Widget
(09:52:10) ColoredBox Widget
(09:53:01) Color Class
(09:56:53) TextStyle
(10:04:22) Colors
(10:06:49) TextField Widget
(10:48:00) Why Build Function Should Contain NO Complex Tasks
(10:53:12) Padding & Container Widget
(11:02:01) Padding vs Margin - The Difference
(11:07:56) TextButton Widget
(11:13:35) Flutter Lints
(11:18:50) TextButton Widget contd.
(11:34:29) ElevatedButton Widget
(11:44:26) AppBar Widget
(11:51:47) StatefulWidget
(12:24:38) Build Function Can Be Called How Many Times?
(12:27:11) setState
(12:41:19) CupertinoApp & iOS Styled Widgets
(12:59:14) initState and dispose
(13:02:05) Recap & Widgets LifeCycle
(13:09:53) Weather App Demo
(13:11:06) Weather App Setup & Default Flutter Code
(13:26:48) GestureDetector & InkWell Widget
(13:29:20) IconButton Widget
(13:30:17) PlaceHolder Widget
(13:34:22) Card Widget
(13:45:35) ClipRRect Widget
(13:47:01) Backdrop and ImageFilter Widget
(13:58:14) Row Widget
(14:07:49) SingleChildScrollView Widget
(14:13:33) Additional Info Section
(14:25:07) Passing Arguments
(14:35:02) http plugin in Flutter
(14:38:12) OpenMapWeather API
(14:44:57) Handling Future in initState
(14:48:05) Extracting Data from API
(15:01:22) Loading Indicator
(15:06:55) FutureBuilder Widget
(15:19:28) AsyncSnapshot
(15:30:25) for loop
(15:39:42) ListView.builder Widget
(15:50:23) Date Formatting using intl
(16:05:35) Layout Principle In Flutter Explained
(16:10:57) Flutter Behind The Scenes, 3 Trees & BuildContext
(16:32:15) Shop App Demo
(16:33:32) Shop App Project Setup (Fonts, Theme, ColorScheme)
(16:52:23) Header (SafeArea Widget)
(16:59:26) Expanded Widget
(17:14:16) Chip Widget
(17:30:17) How Theming Works Behind the Scenes (InheritedWidget)
(17:37:35) Selecting Filter contd.
(17:38:40) Images and Dummy Data
(17:45:12) Displaying Products List on Home Page (Image Widget)
(18:09:51) Designing Product Details Page (Spacer and Flex Widget)
(18:37:33) Navigation & Routing
(18:48:20) How Navigator Works Behind The Scenes? (And State Management)
(18:59:59) BottomNavigationBar Widget
(19:09:10) IndexedStack Widget
(19:11:59) Designing Cart Page (ListTile Widget)
(19:22:38) State Management with Provider, SnackBar
(19:51:20) Dialogs in Flutter
(20:00:18) Provider Extension Methods on BuildContext & Recap
(20:09:55) Flutter Responsive UI (MediaQuery)
(20:33:15) InheritedWidget vs InheritedModel
(20:35:03) Responsive UI in Flutter (LayoutBuilder Widget)
(20:42:01) MediaQuery vs LayoutBuilder
(20:45:24) Challenge: Make Weather App Responsive
(20:45:48) Flutter Widgets Sizing Summary
(20:46:53) Conclusion

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
