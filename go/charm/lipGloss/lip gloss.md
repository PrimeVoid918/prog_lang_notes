| **Layout Goal**        | **Lipgloss Tool**                     | **Mental Translation**                      |
| ---------------------- | ------------------------------------- | ------------------------------------------- |
| **Grid Blocks**        | `.Width()`, `.Height()`, `.Padding()` | Standard CSS Box Model                      |
| **Borders**            | `.Border(lipgloss.NormalBorder())`    | `border: 1px solid;`                        |
| **Vertical Stack**     | `lipgloss.JoinVertical()`             | `flex-direction: column` / Flutter `Column` |
| **Side-by-Side**       | `lipgloss.JoinHorizontal()`           | `flex-direction: row` / Flutter `Row`       |
| **Responsive Scaling** | `tea.WindowSizeMsg` math              | Media Queries / Flutter `LayoutBuilder`     |