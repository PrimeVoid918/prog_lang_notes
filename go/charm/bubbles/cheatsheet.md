# Bubbles Cheat Sheet

A collection of reusable TUI components designed to work with Bubble Tea.

              Your Bubble Tea App
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
       TextInput     List        Table
          │           │           │
          └───────────┼───────────┘
                      ▼
                 Bubble Tea
                      │
                      ▼
                 Terminal UI

## Common Bubbles

| Component    | Purpose                     |
| ------------ | --------------------------- |
| `textinput`  | Single-line text input      |
| `textarea`   | Multi-line text editing     |
| `list`       | Scrollable/selectable lists |
| `table`      | Tabular data                |
| `paginator`  | Pagination                  |
| `progress`   | Progress bars               |
| `spinner`    | Loading/activity indicators |
| `stopwatch`  | Stopwatch                   |
| `timer`      | Countdown timer             |
| `filepicker` | File selection              |
| `cursor`     | Cursor handling             |
| `runeutil`   | Unicode/rune utilities      |
| `viewport`   | Scrollable content          |


## Text Input
conceptually: 
```go
ti := textinput.New()
ti.Placeholder = "Enter your name..."
ti.Focus()
```
forward messages:
```go
m.textInput, cmd = m.textInput.Update(msg)
```
render it:
```go
m.textInput.View()
```

## List
conceptually:
```go
items := []list.Item{
    item{"First"},
    item{"Second"},
    item{"Third"},
}

l := list.New(items, delegate, width, height)
```
then:
```go
m.list, cmd = m.list.Update(msg)
```
render:
```go
m.list.View()
```

## Table
Useful for structured data:
```blob
NAME       AGE     ROLE
Alice      25      Admin
Bob        31      User
Charlie    28      User
```
A table handles things such as:
	rows
	columns
	selection
	navigation
	scrolling
	rendering

## Spinner
useful when something is happening:
```go
⠋ Loading...
⠙ Loading...
⠹ Loading...
⠸ Loading...
```

## Progress

useful for operations with known progress:
```go
Downloading...
████████████████░░░░ 80%
```

## Viewport
Useful when you have more content than fits on screen.

```go
┌───────────────────────────┐
│ Line 1                    │
│ Line 2                    │
│ Line 3                    │
│ Line 4                    │
│ Line 5                    │
│                           │
│          ...              │
└───────────────────────────┘
```