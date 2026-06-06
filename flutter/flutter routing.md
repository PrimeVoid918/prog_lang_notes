## GoRoute
A **single route node** in the app’s route tree.
- Represents **one navigable location**
- Can have **child routes**
- Can act as a **flow anchor**
- Does **not** keep persistent UI (unlike `ShellRoute`)
Think:
> _“A page that can have children.”_
```dart
GoRoute(
  path: '/home',
  builder: (context, state) => const HomePage(),
);
```
- `path` → URL segment
- `builder` → widget for this route
- Stateless by default

Nested Go_Route
```dart
GoRoute(
  path: '/settings',
  builder: (_, __) => const SettingsPage(),
  routes: [
    GoRoute(
      path: 'profile',
      builder: (_, __) => const ProfilePage(),
    ),
  ],
);
/settings
/settings/profile
```
### Important
- Child paths are **relative**
- No leading `/` inside `routes: []`


### ShellRoute 
only when there is shared UI or shared navigation state
A **layout wrapper with its own Navigator** that stays alive while child routes change.
- persistent app bar
- persistent bottom tabs
- persistent drawer
- independent back stack
### When `ShellRoute` is the RIGHT tool

Use `ShellRoute` if the feature:
✅ has **shared UI chrome**  
✅ has **3+ sibling routes**  
✅ needs **internal back behavior**  
✅ should feel like “one mode” of the app
### Examples
- Bottom tab navigation
- Settings → Profile / Security / Billing
- Registration flow with common header
- Auth flow (login / signup / forgot)