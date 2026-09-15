
### 1. Text & True/False

- **`bool`**: Standard `true` or `false`.
    
- **`string`**: Immutable text string.
    
- **`rune`**: A single Unicode character (an alias for `int32`). In Go, strings are made of bytes, but a `rune` represents an actual character like `'A'` or `'🚀'`.
    
- **`byte`**: Raw 8-bit data (an alias for `uint8`). Used when reading raw data files from disk.
    
### 2. Whole Numbers (Integers)

- **`int`**: The default choice for integers. Automatically uses 32-bit on 32-bit machines, or 64-bit on 64-bit machines (like your Arch system).
    
- **`int8`, `int16`, `int32`, `int64`**: Explicitly sized signed integers (can be negative). For example, `int8` ranges from -128 to 127.
    
- **`uint`, `uint8`, `uint16`, `uint32`, `uint64`**: **U**nsigned integers (cannot be negative, starts at 0). Excellent for values that can never be less than zero, like tracking pixels or array indices.
    

### 3. Decimals & Others

- **`float32`, `float64`**: Numbers with decimals. **Always use `float64`** unless you have a specific reason not to.
    
- **`uintptr`**: An unsigned integer large enough to store an uninterpreted memory address pointer. (You won't need this until you do extreme low-level terminal wizardry).
    
- **`complex64`, `complex128`**: Math values for complex numbers containing real and imaginary parts (mostly used in high-end scientific engineering; you can safely ignore this for your TUIs).