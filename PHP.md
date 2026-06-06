# PHP

## connect file

``` php
include 'header.php'; // continues if error
require 'db.php';     // stops if error
```

## Basics

``` php
<?php
    // Output
    echo "Hello, world!";
    
    // Variables (start with $)
    $name = "John";
    $age = 25;

    // Constants
    define("SITE_NAME", "My Website");

    // Comments
    // Single line
    /* Multi-line */
?>
```

## IF Statement

``` php
$score = 80;

if ($score >= 90) {
    echo "Excellent";
} elseif ($score >= 75) {
    echo "Good";
} else {
    echo "Keep trying!";
}
```

## Form Handling

``` php
//HTML FORM
<form method="POST" action="process.php">
  <input type="text" name="username">
  <input type="submit" value="Submit">
</form>

//Process 
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = $_POST["username"];
    echo "Hello, $username!";
}
?>

// connect to db
<?php
$conn = new mysqli("localhost", "root", "", "my_db");

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Connected successfully!";
?>
```

## Functions

```php
function greet($name) {
    return "Hello, $name!";
}
echo greet("Alice");
```

## Arrays

``` php
// Indexed
$fruits = ["apple", "banana"];
echo $fruits[0]; // apple

// Associative
$user = ["name" => "Jane", "age" => 22];
echo $user["name"]; // Jane
```

## PHP Language and Components

``` php
//Variables & Data Types
$var = "text";                      //(string)
$var = 123;                         //(integer)
$var = true;                        //(boolean)
$arr = array("a", "b");             //(array)
$assoc = array("name" => "John");   //(assoc array)

//Superglobals
$_GET       //Form data from URL
$_POST      //Form data (hidden in body)
$_REQUEST   //Combines GET + POST
$_SESSION   //Store user session data
$_COOKIE    //Store small user data
$_SERVER    //Server environment info
```

## Helpful Built-in Functions

``` php
strlen()        //strlen("hello") = 5
strtolower()    //"HELLO" → "hello"
isset()         //Checks if variable exists
empty()         //True if var is empty/null/0/""
explode()       //Splits string into array
implode()       //Joins array into string
```
