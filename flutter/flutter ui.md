
MaterialApp
 └── FeatureProviderScope
     └── Scaffold
         └── SafeArea
             └── Layout Widgets
                 └── UI Widgets

| Flutter      | React / Web    |
| ------------ | -------------- |
| MaterialApp  | `<App />` root |
| Scaffold     | `<Layout />`   |
| Navigator    | React Router   |
| Column / Row | Flexbox        |
| Container    | `<div>`        |
| Theme        | CSS variables  |
| Provider     | Context API    |
| setState     | useState       |
| Widget       | Component      |

| Widget      | Equivalent              | Best use        |
| ----------- | ----------------------- | --------------- |
| `Column`    | flex-column             | vertical layout |
| `Row`       | flex-row                | horizontal      |
| `Stack`     | z-index                 | overlays        |
| `Expanded`  | flex-grow               | fill space      |
| `Container` | div                     | box styling     |
| `Padding`   | padding                 | spacing         |
| `Center`    | center                  | align           |
| `Align`     | text-align / flex-align | alignment       |
| `SizedBox`  | spacer                  | spacing         |

| Widget    | Purpose        |
| --------- | -------------- |
| `Text`    | text           |
| `Icon`    | icons          |
| `Image`   | images         |
| `Card`    | material card  |
| `Divider` | line separator |

| Widget           | Purpose      |
| ---------------- | ------------ |
| `TextField`      | input        |
| `Checkbox`       | checkbox     |
| `Switch`         | toggle       |
| `DropdownButton` | select       |
| `Slider`         | range        |
| `Form`           | form wrapper |

| Widget                 | When to use      |
| ---------------------- | ---------------- |
| `ElevatedButton`       | primary action   |
| `TextButton`           | secondary        |
| `OutlinedButton`       | neutral          |
| `IconButton`           | icon-only        |
| `FloatingActionButton` | main page action |

| Flutter           | React                |
| ----------------- | -------------------- |
| `StatelessWidget` | functional component |
| `StatefulWidget`  | component with state |
| `setState()`      | `useState`           |