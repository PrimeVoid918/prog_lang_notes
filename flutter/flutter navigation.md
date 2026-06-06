Stack = history  
ShellRoute = tabs / layout
GoRoute = node

| Concept           | React Native               | Flutter                              |
| ----------------- | -------------------------- | ------------------------------------ |
| Stack navigator   | `createStackNavigator`     | `Navigator` / `GoRoute`              |
| Tabs              | `createBottomTabNavigator` | `BottomNavigationBar` + `ShellRoute` |
| Drawer            | `createDrawerNavigator`    | `Drawer` / `NavigationRail`          |
| Nested navigators | Nested stacks              | Nested `GoRoute` trees               |
| Screen            | Component                  | Widget                               |
## Tabs in Flutter = `ShellRoute` (this is the key)

In Flutter, **tabs are NOT navigators**.  
They’re **layouts that host multiple stacks**.

That’s why `ShellRoute` exists.
ShellRoute
 ├─ Tab A stack
 ├─ Tab B stack
 ├─ Tab C stack
