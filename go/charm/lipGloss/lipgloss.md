## Colors

```go
lipgloss.Color("205")
lipgloss.Color("#FF00FF")
lipgloss.Color("red")
```

```go
style.Foreground(lipgloss.Color("205"))
style.Background(lipgloss.Color("#1E1E2E"))
```

### Adaptive Colors

```go
lipgloss.AdaptiveColor{
    Light: "#000000",
    Dark:  "#FFFFFF",
}
```

```go
style.Foreground(lipgloss.AdaptiveColor{
    Light: "#000000",
    Dark:  "#FFFFFF",
})
```

---

## Text Styling

```go
style.Bold(true)
style.Italic(true)
style.Underline(true)
style.Strikethrough(true)
style.Faint(true)
style.Blink(true)
style.Reverse(true)
```

### Reset

```go
style.UnsetBold()
style.UnsetItalic()
style.UnsetUnderline()
style.UnsetStrikethrough()
style.UnsetFaint()
style.UnsetBlink()
style.UnsetReverse()
```

---

## Box Model

```go
style.Width(40)
style.Height(10)

style.Padding(1)
style.PaddingTop(1)
style.PaddingBottom(1)
style.PaddingLeft(2)
style.PaddingRight(2)

style.Margin(1)
style.MarginTop(1)
style.MarginBottom(1)
style.MarginLeft(2)
style.MarginRight(2)
```

### Mental Model

```text
Margin
┌──────────────────────────────┐
│                              │
│   Padding                    │
│   ┌──────────────────────┐   │
│   │                      │   │
│   │       Content        │   │
│   │                      │   │
│   └──────────────────────┘   │
│                              │
└──────────────────────────────┘
```

---

## Borders

```go
style.Border(lipgloss.NormalBorder())
```

Built-in border styles:

```go
lipgloss.NormalBorder()
lipgloss.RoundedBorder()
lipgloss.ThickBorder()
lipgloss.DoubleBorder()
lipgloss.HiddenBorder()
```

### Individual Border Sides

```go
style.BorderTop(true)
style.BorderBottom(true)
style.BorderLeft(true)
style.BorderRight(true)
```

### Border Colors

```go
style.BorderForeground(lipgloss.Color("205"))
```

Or individual sides:

```go
style.BorderTopForeground(...)
style.BorderBottomForeground(...)
style.BorderLeftForeground(...)
style.BorderRightForeground(...)
```

---

## Alignment

### Horizontal

```go
style.Align(lipgloss.Left)
style.Align(lipgloss.Center)
style.Align(lipgloss.Right)
```

### Vertical

```go
style.AlignVertical(lipgloss.Top)
style.AlignVertical(lipgloss.Center)
style.AlignVertical(lipgloss.Bottom)
```

### Combined

```go
style.Align(
    lipgloss.Center,
    lipgloss.Center,
)
```

---

## Width / Height

```go
style.Width(40)
style.Height(10)
```

### Maximum Dimensions

```go
style.MaxWidth(80)
style.MaxHeight(20)
```

### Inline Width

```go
style.Inline(true)
```

---

##  Text Rendering

```go
style.Render("Hello")
```

Multiple values:

```go
style.Render(
    "Hello",
    "World",
)
```

### Copy / Modify Styles

```go
newStyle := style.Copy()
```

```go
newStyle = style.Copy().
    Bold(true).
    Foreground(lipgloss.Color("205"))
```

---

##  Joining Components

### Vertical

```go
lipgloss.JoinVertical(
    lipgloss.Left,
    top,
    middle,
    bottom,
)
```

```text
┌──────────────┐
│     Top      │
├──────────────┤
│    Middle    │
├──────────────┤
│    Bottom    │
└──────────────┘
```

### Horizontal

```go
lipgloss.JoinHorizontal(
    lipgloss.Top,
    left,
    right,
)
```

```text
┌──────────┬──────────┐
│   Left   │   Right  │
└──────────┴──────────┘
```

---

## Place

Position content inside a fixed area:

```go
lipgloss.Place(
    width,
    height,
    lipgloss.Center,
    lipgloss.Center,
    "Hello",
)
```

### Horizontal Placement

```go
lipgloss.Left
lipgloss.Center
lipgloss.Right
```

### Vertical Placement

```go
lipgloss.Top
lipgloss.Center
lipgloss.Bottom
```

---

## PlaceHorizontal / PlaceVertical

### Horizontal

```go
lipgloss.PlaceHorizontal(
    width,
    lipgloss.Center,
    content,
)
```

### Vertical

```go
lipgloss.PlaceVertical(
    height,
    lipgloss.Center,
    content,
)
```

---

## Measuring Content

```go
lipgloss.Width("Hello")
lipgloss.Height("Hello")
```

Useful when calculating layouts.

```go
width := lipgloss.Width(content)
height := lipgloss.Height(content)
```

---

## Truncation

```go
lipgloss.NewStyle().
    MaxWidth(20).
    Render(text)
```

### Explicit Truncation

```go
lipgloss.Truncate(
    text,
    20,
    "...",
)
```

---

## Newline / Multi-line Handling

```go
lipgloss.NewStyle().
    Width(40).
    Render(multilineText)
```

Useful helpers:

```go
lipgloss.Height(text)
lipgloss.Width(text)
```

These account for terminal display width rather than simply using:

```go
len(text)
```

---

## Terminal Integration

Bubble Tea provides terminal dimensions:

```go
case tea.WindowSizeMsg:
    m.width = msg.Width
    m.height = msg.Height
```

Then:

```go
style.Width(m.width)
style.Height(m.height)
```

Or calculate layout:

```go
contentWidth := m.width / 2
```

---

## Style Composition

Styles can be chained:

```go
style := lipgloss.NewStyle().
    Bold(true).
    Foreground(lipgloss.Color("205")).
    Background(lipgloss.Color("235")).
    Padding(1, 2).
    Margin(1).
    Border(lipgloss.RoundedBorder())
```

Then:

```go
style.Render("Hello")
```

---

## Style Inheritance / Merging

```go
base := lipgloss.NewStyle().
    Bold(true).
    Padding(1)

accent := base.Copy().
    Foreground(lipgloss.Color("205"))
```

---

##  Underline / Border Color

```go
style.Underline(true)
style.UnderlineSpaces(true)
```

```go
style.BorderForeground(color)
```

---

## Gradient / Color Utilities

Useful color helpers:

```go
lipgloss.CompleteColor()
lipgloss.NoColor{}
lipgloss.AdaptiveColor{}
```

Terminal color profile:

```go
lipgloss.DefaultRenderer()
```

---

## Renderer

Get the renderer:

```go
renderer := lipgloss.DefaultRenderer()
```

Create a renderer:

```go
renderer := lipgloss.NewRenderer(os.Stdout)
```

Create styles from a renderer:

```go
style := renderer.NewStyle()
```

---

##  Common Layout Patterns

### Two Columns

```go
left := leftStyle.Render(leftContent)
right := rightStyle.Render(rightContent)

view := lipgloss.JoinHorizontal(
    lipgloss.Top,
    left,
    right,
)
```

### Header / Body / Footer

```go
view := lipgloss.JoinVertical(
    lipgloss.Left,
    header,
    body,
    footer,
)
```

### Centered Box

```go
box := lipgloss.NewStyle().
    Width(40).
    Height(10).
    Border(lipgloss.RoundedBorder()).
    Align(lipgloss.Center).
    AlignVertical(lipgloss.Center).
    Render("Hello")
```

Then:

```go
view := lipgloss.Place(
    width,
    height,
    lipgloss.Center,
    lipgloss.Center,
    box,
)
```

---

# Translation

|Goal|Lip Gloss|
|---|---|
|Text color|`.Foreground()`|
|Background|`.Background()`|
|Bold|`.Bold(true)`|
|Italic|`.Italic(true)`|
|Underline|`.Underline(true)`|
|Box width|`.Width()`|
|Box height|`.Height()`|
|Padding|`.Padding()`|
|Margin|`.Margin()`|
|Border|`.Border()`|
|Border color|`.BorderForeground()`|
|Horizontal alignment|`.Align()`|
|Vertical alignment|`.AlignVertical()`|
|Stack vertically|`JoinVertical()`|
|Place side-by-side|`JoinHorizontal()`|
|Center in area|`Place()`|
|Measure text|`Width()` / `Height()`|
|Responsive layout|`tea.WindowSizeMsg` + calculations|
|Light/dark colors|`AdaptiveColor`|
|Reuse style|`.Copy()`|
|Render|`.Render()`|
