| **Keyword**   | **Category**  | **Short Description**                                                                          |
| ------------- | ------------- | ---------------------------------------------------------------------------------------------- |
| `package`     | Organization  | Defines the namespace/package this file belongs to.                                            |
| `import`      | Organization  | Pulls in external or standard library packages.                                                |
| `func`        | Declarations  | Declares a function or a method.                                                               |
| `var`         | Declarations  | Declares a variable with a specific type.                                                      |
| `const`       | Declarations  | Declares a constant (read-only) value.                                                         |
| `type`        | Declarations  | Declares a new custom user-defined type (like a `struct`).                                     |
| `struct`      | Declarations  | Defines a collection of fields (like a schema or object shape).                                |
| `interface`   | Declarations  | Defines a set of method signatures for behavior matching.                                      |
| `map`         | Declarations  | Declares a hash table / dictionary data structure.                                             |
| `chan`        | Concurrency   | Declares a channel used to pass data safely between Goroutines.                                |
| `go`          | Concurrency   | Starts a new concurrent Goroutine (lightweight thread).                                        |
| `select`      | Concurrency   | Waits on multiple channel communication operations.                                            |
| `if`          | Control Flow  | Standard conditional statement.                                                                |
| `else`        | Control Flow  | Executed if the `if` condition evaluates to false.                                             |
| `switch`      | Control Flow  | Starts a conditional block to match multiple values or cases.                                  |
| `case`        | Control Flow  | Defines an individual matching block inside a `switch` statement.                              |
| `default`     | Control Flow  | The fallback option inside a `switch` statement if no cases match.                             |
| `for`         | Loops         | The **only** loop keyword in Go (used for standard, while, and infinite loops).                |
| `range`       | Loops         | Iterates over elements in a **slice**, array, map, string, or channel.                         |
| `break`       | Loops/Control | Breaks out of the current loop or switch block early.                                          |
| `continue`    | Loops         | Skips the rest of the current loop iteration and moves to the next.                            |
| `return`      | Functions     | Exits a function and optionally returns specified values.                                      |
| `defer`       | Lifecycle     | Delays the execution of a function until the surrounding function returns (great for cleanup). |
| `fallthrough` | Control Flow  | Forces execution to move to the next sequential case in a `switch` block.                      |
| `goto`        | Control Flow  | Jumps directly to a labeled execution point elsewhere in the function.                         |
