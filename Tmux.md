## Session Survival

| Key           | Action              |
| ------------- | ------------------- |
| `Ctrl+b d`    | Detach from session |
| `tmux attach` | Reattach session    |
| `tmux ls`     | List sessions       |
| `Ctrl+b s`    | Session picker      |
**Why:** This is the whole reason tmux exists.

---
## Window Navigation (Tabs)

| Key          | Action                |
| ------------ | --------------------- |
| `Ctrl+b c`   | New window            |
| `Ctrl+b n`   | Next window           |
| `Ctrl+b p`   | Previous window       |
| `Ctrl+b 1-9` | Jump to window number |
| `Ctrl+b ,`   | Rename window         |
| `Ctrl+b &`   | Kill window           |
**Think:** Windows = tabs.

---
## Pane Management (Splits)

| Key            | Action             |
| -------------- | ------------------ |
| `Ctrl+b %`     | Vertical split     |
| `Ctrl+b "`     | Horizontal split   |
| `Ctrl+b ←→↑↓`  | Move between panes |
| `Ctrl+b x`     | Kill pane          |
| `Ctrl+b z`     | Zoom/unzoom pane   |
| `Ctrl+b Space` | Cycle layouts      |
**Think:** Panes = splits inside a tab.

---
## Scrolling

| Key        | Action                |
| ---------- | --------------------- |
| `Ctrl+b [` | Enter scrollback mode |
| `q`        | Exit scrollback       |
| `/`        | Search forward        |
| `?`        | Search backward       |
This is the second-biggest reason people use tmux.

---
# Tier 2 — Very Useful (Learn Next)

## Pane Discovery

| Key        | Action            |
| ---------- | ----------------- |
| `Ctrl+b q` | Show pane numbers |
| `Ctrl+b w` | Window chooser    |
When you have lots of panes/windows.

---
## Copy & Paste
Inside copy mode:

| Key     | Action          |
| ------- | --------------- |
| `Space` | Begin selection |
| `Enter` | Copy selection  |

Outside copy mode:

| Key        | Action |
| ---------- | ------ |
| `Ctrl+b ]` | Paste  |

---
## Command Mode

| Key        | Action                   |
| ---------- | ------------------------ |
| `Ctrl+b :` | Open tmux command prompt |
Examples:
```bash
new-window
split-window -h
kill-pane
```
Very powerful when you forget keybindings.

---
# Tier 3 — Power User
## Rearranging Panes

| Key        | Action               |
| ---------- | -------------------- |
| `Ctrl+b {` | Move pane left/up    |
| `Ctrl+b }` | Move pane right/down |

---
## Synchronized Panes
```bash
Ctrl+b :
setw synchronize-panes on
```
Everything typed gets sent to all panes.

Useful for:
- Multiple SSH servers
- Docker containers
- Kubernetes nodes
---
## Marking Panes

| Key        | Action    |
| ---------- | --------- |
| `Ctrl+b m` | Mark pane |
| `Ctrl+b '  | Jump back |

---
# Tier 4 — Rare but Nice

| Key              | Action            |
| ---------------- | ----------------- |
| `Ctrl+b t`       | Clock             |
| `Ctrl+b $`       | Rename session    |
| `Ctrl+b ?`       | Show bindings     |
| `tmux list-keys` | Dump all bindings |

---
# Mental Model
```bash
tmux
└── Session
    ├── Window (tab)
    │   ├── Pane (split)
    │   ├── Pane (split)
    │   └── Pane (split)
    │
    ├── Window
    └── Window
```

Remember:
```
Session = workspace/project

Window = tab

Pane = split
```

For example:
```bash
Session: work

Window 1: editor
    Pane 1: nvim
    Pane 2: terminal

Window 2: docker

Window 3: logs
```

---
# My "Arch + Kitty + Neovim" Minimal Set

If I could only keep **8 bindings**:
```bash
Ctrl+b d      detach
Ctrl+b s      switch session

Ctrl+b c      new window
Ctrl+b 1-9    jump window

Ctrl+b %      vertical split
Ctrl+b "      horizontal split
Ctrl+b arrows move pane

Ctrl+b z      zoom pane
Ctrl+b [      scrollback mode
```

Those alone cover almost every workflow: coding, logs, SSH, Docker, servers, and note-taking.