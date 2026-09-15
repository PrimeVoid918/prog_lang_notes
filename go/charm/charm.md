# 🍬 The Charm Ecosystem: Modern Go TUI Stack

**Charm** (or Charmbracelet) is a suite of modular, open-source Go libraries designed to build beautiful, interactive, and modern Terminal User Interfaces (TUIs). Instead of one massive framework, Charm splits the work into specialized, highly composable tools.

## 🏗️ The Core Architecture

To build a Charm-based app, you combine three primary layers:

### 1. The Engine: **Bubble Tea** (`bubbletea`)
* **What it does:** Manages your application's state, user input, and lifecycle.
* **How it works:** It uses **The Elm Architecture** workflow. Every app is broken down into three strict steps:
    * `Init()`: What happens when the app starts.
    * `Update()`: How the app responds to events (key presses, mouse clicks, ticks).
    * `View()`: How the app renders the current state into a string.

### 2. The Paintbrush: **Lip Gloss** (`lipgloss`)
* **What it does:** Handles all styling, colors, layout alignment, and borders.
* **How it works:** It brings CSS-like styling to the terminal. You define reusable styles (margins, padding, adaptive light/dark mode colors) and apply them to raw strings inside your View.

### 3. The Blueprint Catalog: **Bubbles** (`bubbles`)
* **What it does:** Provides a library of ready-to-use UI components.
* **How it works:** Instead of coding common UI elements from scratch, you import them from Bubbles. Each component is written in Bubble Tea and Lip Gloss, meaning they hook directly into your main app's engine loops.
* **Popular components:** Text inputs, spinners, progress bars, paginated lists, and file pickers.

---

## 🔄 How They Interact (Mental Model)

```text
       [ User Input / Events ]
                 │
                 ▼
┌─────────────────────────────────┐
│       1. BUBBLE TEA             │ <── Hooks into internal component loops
│       (The Core Engine)         │
└────────────────┬────────────────┘
                 │ Passes state to
                 ▼
┌─────────────────────────────────┐
│       2. BUBBLES                │ <── Renders pre-made interactive parts
│       (The UI Components)       │
└────────────────┬────────────────┘
                 │ Styled & positioned by
                 ▼
┌─────────────────────────────────┐
│       3. LIP GLOSS              │ <── Formats text, colors, and margins
│       (The Layout & Style)      │
└─────────────────────────────────┘
                 │
                 ▼
         [ Terminal Screen ]
```
