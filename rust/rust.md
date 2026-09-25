## comments
```rust
// single line

/* multiple lines

*/
```

--- 
## Var Declarations
```rust 
// let <name> = <value>;
// let <name>: <type> = <value>;
let age = 24; // rust variables are immutable by default.

// age = 25; // ❌ cannot mutate immutable variable

let mut age = 24; // mutable variable:

age = 25;

// let // immutable binding 
// let mut // mutable binding

```

---
## Data Types
```rust
// i8
// i16
// i32
// i64 
// i128 
// isize 
// u8 
// u16 
// u32 
// u64 
// u128 
// usize

// int
// i = signed integer
// u = unsigned integer
// number = bit width
let signed: i32 = -100;
let unsigned: u32 = 100;

// float
// f32
// f64
let x: f32 = 3.14;
let y: f64 = 3.141592653589793;

// bool
let running: bool = true;
let finished: bool = false;

// char
// 'A'     // char
// "A"     // string slice
let letter: char = 'A';
let emoji: char = '🦀';

// two important string types
// String
// &str
let name = String::from("Prime"); // String owns its string data.
let name: &str = "Prime"; // &str is a borrowed string slice.

```

## Data Structures 
``` rust
// tuples
// accessed by positions
// user.0
// user.1
// user.2

let user = ("Prime", 24, true); // init
let (name, age, active) = user; // destructuring

// array
// [type; size] // syntax
// numbers[0] // access
let numbers = [1, 2, 3, 4, 5]; // fixed-size collection
let numbers: [i32; 5] = [1, 2, 3, 4, 5]; // explicit type
// mutate
let mut numbers = [1, 2, 3];
numbers[0] = 10;

// vector
let mut numbers: Vec<i32> = Vec::new(); // dynamic collection

numbers.push(10);
numbers.push(20);
// or
let numbers = vec![1, 2, 3, 4, 5];

numbers[0] // access

// constants
const MAX_USERS: u32 = 100; // constants require an explicit type

// type conversion
// <value> as <type>  // syntax
let x: i32 = 10;
let y: i64 = x as i64;
let x = 10u32;
let y = x as i64;

```

## Operators
```rust
// +
// -
// *
// /
// %
let x = 10;
let y = 3;
x + y
x - y
x * y
x / y
x % y

// comparison
// ==
// !=
// >
// <
// >=
// <=

// logical
// &&  // AND
// ||  // OR
// !   // NOT

// assignment
// =
// +=
// -=
// *=
// /=
// %=
```

## Control Flow
```rust
// if
if condition {
    // block
} else if condition {
    // block
} else {
    // block
}
// if is an expression 
let result = if x > 10 {
    "large"
} else {
    "small"
};

// loop
loop {
    // block
}
loop {
    if condition {
        break;
    }
}
loop {
    if condition {
        continue;
    }
}

// while 
while condition {
    // block
}

// for
for item in collection {
    // block
}
for i in 0..10 {
    println!("{i}");
}
for i in 0..=10 {
    println!("{i}");
}



```

## Functions
``` rust
fn <name>() {
    // block
}
fn greet(name: &str) {
    println!("Hello {name}");
}
fn add(a: i32, b: i32) -> i32 {
    a + b
}

fn add(a: i32, b: i32) -> i32 { //can return the final expression without return
    a + b
}
fn add(a: i32, b: i32) -> i32 { // or explicit
    return a + b;
}
// semicolon changes the meaning
fn add(a: i32, b: i32) -> i32 { 
    a + b       // returns value
}
fn add(a: i32, b: i32) -> i32 {
    a + b;      // statement; does NOT return the value
}




```

## ??
### Structs
``` rust
// structs
struct User {
    name: String,
    age: u32,
}
let user = User { // craeate
    name: String::from("Prime"),
    age: 24,
};
// access
user.name
user.age
let mut user = User {// mutable struct
    name: String::from("Prime"),
    age: 24,
};
user.age = 25; // mutate
```
### Imp
```rust
struct User {
    name: String,
}

impl User { // attach behavior to a struct
    fn greet(&self) {
        println!("Hello {}", self.name);
    }
    fn sample &self {
	    //
    }
}

// usage
let user = User {
    name: String::from("Prime"),
};

user.greet();

```

### Visibility
```rust 
pub struct User {
    pub name: String,
    age: u32,
}

pub fn public_function() {
}

fn private_function() {
}

```

### Enums
```rust
enum Direction {
    Up,
    Down,
    Left,
    Right,
}

// usage
let direction = Direction::Up;

// can contain data
enum Message {
    Quit,
    Write(String),
    Move {
        x: i32,
        y: i32,
    },
}

```

### Match
```rust
// patttern matching
match direction {
    Direction::Up => println!("Up"),
    Direction::Down => println!("Down"),
    Direction::Left => println!("Left"),
    Direction::Right => println!("Right"),
}

```

### ?
#### Option
```rust
// rust does not use `null` as the normal representation of an optional value.
// Option<T>
// Some(value)
// None

let name: Option<String> = Some(String::from("Prime"));
let nothing: Option<String> = None;

// pattern matchin
match name {
    Some(value) => println!("{value}"),
    None => println!("No value"),
}
```
#### Result
```rust
// rsed for operations that can succeed or fail
// Result<T, E>
// Ok(value)
// Err(error)
fn divide(a: i32, b: i32) -> Result<i32, String> {
    if b == 0 {
        Err(String::from("Cannot divide by zero"))
    } else {
        Ok(a / b)
    }
}
```

## pointers ??
### References
``` rust 
// &T     // immutable reference:
// &mut T // Mutable reference:
fn print_name(name: &String) {
    println!("{name}");
}

// Borrowing
let name = String::from("Prime"); 
print_name(&name); // function gets access to name without taking ownership of it.

```
### Ownership
```rust 
let name = String::from("Prime"); // name owns the String

// moving name -> other
let name = String::from("Prime");
let other = name;
// println!("{name}"); // ❌
println!("{other}");   // ✅

// example
let name = String::from("Prime");
let reference = &name;

println!("{reference}");
println!("{name}");


```