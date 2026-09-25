# Bubble Tea Cheat Sheet
Go framework for building terminal user interfaces (TUIs).
Core idea:

       Event / Message
              │
              ▼
       ┌─────────────┐
       │   Update()  │
       └──────┬──────┘
              │
        changes state
              │
              ▼
       ┌─────────────┐
       │   View()    │
       └──────┬──────┘
              │
              ▼
        Terminal UI

## Elm Architecture
A Bubble Tea application revolves around three methods:

```go
type Model struct {
    // application state
}

func (m Model) Init() tea.Cmd {
    return nil
}

func (m Model) Update(msg tea.Msg) (tea.Model, tea.Cmd) {
    return m, nil
}

func (m Model) View() string {
    return "Hello!"
}
```

### Model
The model contains the application's state.
```go
type Model struct {
    cursor int
    items  []string
    width  int
    height int
}
```


### Init()
Runs when the program starts.
returns an optional tea.Cmd.
```go
func (m Model) Init() tea.Cmd {
    return nil
}
```

Example:
```go
func (m Model) Init() tea.Cmd {
    return tick()
}
```

### Update()
Receives messages and changes the model.
```go
func (m Model) Update(msg tea.Msg) (tea.Model, tea.Cmd) {
    switch msg := msg.(type) {

    case tea.KeyMsg:
        switch msg.String() {
        case "q":
            return m, tea.Quit
        }

    }
    return m, nil
}
```


### View()
Turns the current state into terminal output.
```go
func (m Model) View() string {
    return lipgloss.NewStyle().
        Bold(true).
        Render("Hello!")
}
```


### Messages
A tea.Msg represents an event.

Common examples:
	tea.KeyMsg
	tea.MouseMsg
	tea.WindowSizeMsg
	tea.FocusMsg
	tea.BlurMsg

You can also create your own:
```go
type dataLoadedMsg struct {
    data []string
}
```
Then handle it:
```go
case dataLoadedMsg:
    m.items = msg.data
```

## Mental model:
Something happens
      ↓
   tea.Msg
      ↓
   Update()
      ↓
 state changes
      ↓
   View()

## Keyboard Input

Basic key handling:
```go
case tea.KeyMsg:
    switch msg.String() {
    case "q":
        return m, tea.Quit

    case "up", "k":
        m.cursor--

    case "down", "j":
        m.cursor++
    }
```

#### Useful key values:
"enter"
"esc"
"tab"
"space"
"up"
"down"
"left"
"right"
"home"
"end"
"pgup"
"pgdown"
"ctrl+c"
"ctrl+q"


## Quitting
The simplest way:
```go
return m, tea.Quit
```


##  Commands

A tea.Cmd represents an operation that happens outside the immediate Update() logic.
Conceptually:
```go
type Cmd func() tea.Msg
```

Example:
```go
func getData() tea.Cmd {
    return func() tea.Msg {
        return dataLoadedMsg{
            data: []string{"one", "two", "three"},
        }
    }
}
```

Then:
```go
func (m Model) Init() tea.Cmd {
    return getData()
}
```

When the command finishes, Bubble Tea sends the returned message to Update().

## Commands + Messages

             ┌──────────────┐
             │    Update    │
             └──────┬───────┘
                    │
                    │ returns Cmd
                    ▼
             ┌──────────────┐
             │     Cmd      │
             │  does work   │
             └──────┬───────┘
                    │
                    │ returns Msg
                    ▼
             ┌──────────────┐
             │    Update    │
             └──────┬───────┘
                    │
                    ▼
                new state


## Window Size
Bubble Tea sends a tea.WindowSizeMsg when the terminal size changes.
```go
case tea.WindowSizeMsg:
    m.width = msg.Width
    m.height = msg.Height
```

This is especially useful with Lip Gloss:
```go
style := lipgloss.NewStyle().
    Width(m.width).
    Height(m.height)
```


## Mouse Input
Mouse events can be handled through tea.MouseMsg.
Conceptually:
```go
case tea.MouseMsg:
    // inspect mouse event
```

Mouse support needs to be enabled when starting the program.
Use mouse input when your TUI actually benefits from it; keyboard-driven interfaces are often simpler.
