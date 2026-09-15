```go
package main

import "os"

// 1. TYPES AT THE TOP
type ZoxideDirContents struct {
	Info os.FileInfo
}

// 2. PRIMARY EXPORTED/MAIN FUNCTIONS
func ReadDir(dir string) ([]ZoxideDirContents, error) {
    // Core logic...
    // Calls helper functions below
}

// 3. UTILITY/HELPER FUNCTIONS AT THE BOTTOM
func formatFilename(name string) string {
    // Small formatting helper
    return name
}

```