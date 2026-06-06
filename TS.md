# TS

## Variables

``` typescript
let myVar : type = value;

let myVar : string = "value";
myVar = 12 //error type conversion during mutation
```

### Type Guards

``` typescript
typeof      // returns a string of type
instanceof  // returns bool
```

### Primitive Types

- number
- string
- boolean
- null
- undefined

### Type Inference

automatically determin the type of a variable based on its values

``` typescript
let myVar1 = 12 //number
myVar1 = "12" //error in mutation -> Type 'string' is not assignable to type 'number'.

let myVar2 = "12"; //string
myVar2 = 12;  //error in mutation -> Type 'number' is not assignable to type 'string'.

// use "typeof" operator to know what kind of data
let var1 = 12;
typeof(var1);       //number
let var2 = "12";
typeof(var2);       //string
let var3 = true;
typeof(var3);       //boolean
let var4 = null;
typeof(var4);       //object
let var5 = undefined;
typeof(var5);       //undefined
let var6 = {};
typeof(var6);       //object
let var7 = [];
typeof(var7);       //object
let var8 = ()=>{};
typeof(var7);       //function

// you can use any for loose typing
let var8:any = 12;
var8 = "12" //will not cause an err
//#! using :any is not a good practice
```

## Functions

### Function Paramater Anotations

``` typescript
//basic structure

/*
    fn <name>(params: type): <returnType> {
        return {argument};
    }
*/

//ex
function add(params: number): number{
    return params + 1;
}

const b : number = add(2);

console.log(b);
```

### Return Annotations

``` typescript
//follows similar primitive data type
//:void returns nothing
//:any specifically any !not reccomended
//:never, wako kibaw
function hello() : void{
    console.log("Hello world");
}

hello();
```

## Data Structures

### Array Types

``` typescript
// two ways to make a type
// type[]
// Array[type]

let arr : Array<number> = [1,2,3,4,5]
let arr2 : number[] = [6,7,8,9,10];

console.log(arr);
console.log(arr2);

// 2D arr
// Array<Array<number>>
// type[][]
let arr : Array<Array<number>> = [[1,2,3],[3,4,1,2]]
let arr2 : number[][] = [[6,7,8],[9,10,1,2]]

for(let a = 0; a<arr.length; a++){
    const tempArr:Array<number> = [];
    for(let b = 0; b<arr[a].length; b++){
        tempArr.push(arr[a][b]);
    }
    console.log(tempArr);
    // [ 1, 2, 3 ]
    // [ 3, 4, 1, 2 ]
}

```

### Objects

``` typescript
/* 
Annotation varName { 
    propName: type 
}
*/

interface Box{ //type aliases
    width: number;
    height: number;
}

function defineBox(box: Box): void {
    console.log(`box width is ${box.width}, height is ${box.height}`);
}

const boxer: Box = {
    width: 12,
    height: 13
}

defineBox(boxer);

```

## Type Aliases

``` typescript
/* type <name> {
        propName: type
    }
*/
```

### Intersection Types

``` typescript
// mixes type aliasas props
// props can cause conflicts!

// Type1 & Type2

type Steam = {
    userName: string,
    hoursPlayed: number
}
type Playstore = {
    faveGame: string,
    totalSkins: number
}

const gamer : Steam & Playstore = {
    userName: "Maxxer",
    hoursPlayed: 12,
    faveGame: "ML",
    totalSkins: 123
}

console.log(gamer);
```

### Unions

``` typescript
// uses | or pipe

const loginName: number | string = 1232231      // can contain number and strings
const loginName: number | string = true         // will throw and error 

// also includes objects such as arrays
const loginName: number | string | Array<number> = [1,2]         // will throw and error 

// also applicable in arrays
const arr: Array<string | number> = [1,2,"3","4"]

// also applicable in type aliases
type Customer = {
    login: string | number;
}
const customerLogin: Customer = {login: 12345}
const customerLogin: Customer = {login: "sample@gmail"}

// also applicable to combine two aliases
// rule: prop in A should match prop in B
//       it cannot mix and match

type A = {
    Aa: string,
    Ab: string,
    Ac: string
}
type B = {
    Ba: string,
    Bb: string
}

// Type '{ Aa: string; Ab: string; }' is not assignable to type 'A | B'.
// Property 'Ac' is missing in type '{ Aa: string; Ab: string; }' but required in type 'A'.ts
const Comb: A|B = {Aa:"123", Ab:"123"}

// Type '{ Aa: string; Bb: string; }' is not assignable to type 'A | B'.
// Property 'Ba' is missing in type '{ Aa: string; Bb: string; }' but required in type 'B'.
const Comb: A|B = {Aa:"123", Bb:"123"}
```

### Literal Types

``` typescript
// similar to enums, the value becomes a type and will throw an error if it does not exist
// should be declared in `let` as the next value checks if it exists in the type

let numbers : 1|2|3|4|5;

// Type '7' is not assignable to type '1 | 2 | 3 | 4 | 5'.
console.log(numbers = 7);

// can be applied to any types but bool behaves like this
let isTrue : true;
isTrue = true;      //✅
isTrue = false;     //Type 'false' is not assignable to type 'true'.
```

### Tuples

``` typescript
// similar to python, a set of a fixed number of elements, immutable
// it is similar to arrays, but they have a specific structure and can be used to model finite with known lengths
// allows option property .?

let myTuple: [string, number] = ["Hello", 2];
console.log(myTuple[0]);        //Hello
console.log(myTuple[1]);        //2

// Type '[string, number, number]' is not assignable to type '[string, number]'.
// Source has 3 element(s) but target allows only 2.ts(2322)
let myTuple: [string, number] = ["Hello", 2, 3];

console.log(myTuple[3]);        // Tuple type '[string, number]' of length '2' has no element at index '3'.

// Destructuring Individual Elements
let [first, second] = myTuple;
let [one, two] = myTuple;

console.log(first, second);     //Hello 2
console.log(one, two);          //Hello 2

// 2D Grid (Matrix)
let grid: [number,number][] = [
        [0,0],[1,0],
    [0,1],[1,1],
]
let grid: Array<Array<number>> = [
    [0,0],[1,0],
    [0,1],[1,1],
]
```

### Enums

``` typescript
// A way to define a set of named constants
// Allows you to define a collection of related values that can be used interchangably in your code

enum WeatherCondition {
    Sunny,  //->0
    Cloudy, //->1
    Rainy,  //->2
    Snow    //->3
}

const WeatherRN = WeatherCondition.Cloudy   // 0
WeatherCondition[1]                         // Cloudy

```

### Class Properties Annotations

``` typescript
class Person {              //      immutable           //      private         //      protected->can be accessed by subclass
    protected name: string; // readonly name: string    // private name: string //  protected name: string
    protected age: number;  // readonly age: number     // pricate age: number  //  protected name: string


    constructor(name: string, age: number){
        this.name = name;
        this.age = age;
    }

    get getName():string{           // public get getName():string{
        return this.name;
    }

    set setName(name:string){       // public set setName():string{
        this.name = name;
    }
}

// Subclass that extends Person
class Employee extends Person{
    private jobTitle: string;

    constructor(name: string, age:number, jobTitle: string){
        super(name, age); // Call the constructor of the base class
        this.jobTitle = jobTitle
    }

    public get getDetails():string {
        // Accessing protected members from the base class
        return `${this.getName}, Age: ${this.age}, Job Title: ${this.jobTitle}`;
    }
}

const employee = new Employee("Alice", 90, "JS Senior Dev");
console.log(employee); //Employee { name: 'Alice', age: 90, jobTitle: 'JS Senior Dev' }
```

## Interface

``` typescript
// basic structure
/*
    interface <name>{
        prop1: type;
        prop2: type;
    }
*/

// interface definition
interface Person {
    name: string;
    age: number;
}

// usage
const person: Person = { name: "Agatha", age: 12};
console.log(person); // { name: 'Agatha', age: 12 }

// interface of an class
interface Vehicle {
    start(): void;
    stop(): void;
}

class Car implements Vehicle{
    start(){
        console.log("Car is starting ....");
    }
    stop(){
        console.log("Car is stopping ....");
    }
}

// usage
const car1 = new Car();
car1.start();
car1.stop();

// interfaces in function                   -> not that applicable in function declaration
interface SampFunct {
    (a:number,b:number) : number
}

const add: SampFunct = (a,b) => a+b         // best in arrow functions
console.log(add(1,2))

// Declaration Merging / Interface Extension
// once interface is defined it cannot be modified

// Original Declaration
interface Car{
    brand: string;
    start(): void;
}

// Declaration Merging (interface extension)
interface Car {
    model: string;
    stop(): void;
}

// Usage of the etended interface
const MyCar: Car = {
    brand: "Toyota",
    model: "Cammy",
    start(): { console.log("Starting") },
    stop(): { console.log("Stopping") }
}
```

## Generics

``` typescript
// basic syntax
/*
    function funcName <T> (param: T): ReturnType {}
    // T -> Type Parameter Placeholder
        // Any name such as T, U, V, TypeA can be used within function signiture body

    // Param: T -> Type Annotation
                // Type (T) is applied tp function arguments

    // ReturnType -> cam use type parameter for its return type

*/

function sample<T> (a:T): T {
    return a
}

const res = sample<string>("e")

// Handle Multiple Type Dynamically
function Pair <T, U> (a:T, b:U): [T,U] {
    return [a, b]
}

const mixedPair = Pair<string, number>("eli", 24)

// Constants
interface A {
    a: number
}
interface B extends A {
    b: number
}

function PrintMe <T extends B>(x:T): string {
    return `a: ${x.a}, b: ${x.b}`
}

console.log(PrintMe({a: 10, b:20}))

// function
function filterFunc <T> (arr: Array<T>, condition: (item: T) => boolean) : Array<T> {
    return arr.filter( (item) => condition(item) );
}

const numArr = [1,2,3,4,5,6,7]
const evenNum = filterFunc<number>(numArr, (num) => num % 2 === 0);

// Generics in Classes
class Box<T> {
    private content: T;

    constructor (initContent: T){
        this.content = initContent;
    }

    getContent (): T {
        return this.content
    }

    setContent(newContent: T): void {
        this.content = newContent
    }
}
```
