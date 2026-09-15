```go
package mypackage

// 1. Structs
type User struct {}  // Public: Other packages can create a User
type secret struct {} // Private: Hidden from other packages

// 2. Struct Fields (Crucial for JSON and databases!)
type Profile struct {
    Name string // Public: Other packages can read/write this field
    age  int    // Private: Hidden; only code in 'mypackage' can see it
}

// 3. Functions & Methods
func DoSomething() {}       // Public function
func doInternalWork() {}    // Private function
func (p Profile) Greet() {} // Public method
func (p Profile) speak() {} // Private method

// 4. Variables & Constants
const ExportedConfig = "v1" // Public constant
const localConfig = "debug" // Private constant
var TopScore int            // Public variable
var currentScore int        // Private variable

```