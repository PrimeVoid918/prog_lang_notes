```go
package main // mandatory

import "fmt" // "Format" package for printing text

func main() { // mandatory function
    fmt.Println("Hello, TUI World!")
}
```

### Variables 
```go
// Type inference (Go guesses it's a string and an int)
// Function scope applicatble only
appName := "MyTUI" 
version := 1
    
// Explicit variable declaration (useful for empty/default states)
var userChoice string 
var isRunning bool = true

// An empty slice of strings 
var menuOptions []string 
// Add items using append() 
menuOptions = append(menuOptions, "Home", "Settings", "Quit") 
// Access by index (0-based) 
firstOption := menuOptions[0] // "Home"
```

### Control Flow
```go
func handleKey(key string) {
    switch key {
    case "q", "ctrl+c":
        fmt.Println("Exiting app...")
    case "up":
        fmt.Println("Move cursor up")
    default:
        fmt.Println("Unknown key")
    }
}

```

### Structs
```go
// Define the shape of your data
type TodoItem struct {
    Title string
    Done  bool
}

func main() {
    // Create an instance of your data
    item := TodoItem{
        Title: "Fix UI layout bug",
        Done:  false,
    }
    
    // Read or change the data
    item.Done = true 
}

```
### Loops
go has only one loop keyword
`for range`
```go
options := []string{"View Pods", "View Logs", "Exit"} 

// i = index, opt = the string value 
for i, opt := range options { 
	// %d prints an integer, %s prints a string 
	fmt.Printf("[%d] %s\n", i+1, opt) 
}
```

### Pointers
```go
type UIState struct {
    CursorPos int
}

// The '*' means this function takes a reference, not a copy
func moveDown(state *UIState) {
    state.CursorPos++ // Modifies the original state directly!
}

func main() {
    myState := UIState{CursorPos: 0}
    
    // The '&' passes the memory address of myState
    moveDown(&myState) 
    
    fmt.Println(myState.CursorPos) // Prints: 1
}
```