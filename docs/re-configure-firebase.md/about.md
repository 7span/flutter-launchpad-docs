---
sidebar_position: 1
--- 

# Re-Configure Firebase

- First login to your firebase account by hitting the following command to the terminal.

```
firebase login
```

:::warning
If you want to change the current logged-in account first run **firebase logout** command followed by **firebase login** command.
:::

- We will re-configure the firebase setup using FlutterFire CLI, so make sure you have activated it using following command.

```
dart pub global activate flutterfire_cli
```

:::info 
- We have kept the same bundle id for all iOS flavors so that we do not have to create multiple applications in the App Store for test flight purposes.
:::

- Run this command one-by-one in the terminal to configure all applications.

### Development config with Debug-dev build config
```dart
sh scripts/firebase_setup.sh development
```

### Staging config with Debug-stg build config
```dart
sh scripts/firebase_setup.sh staging 
```

### Production config with Debug-prod build config
```dart
sh scripts/firebase_setup.sh
```

:::note
To understand re-config flavors in-depth head over to this [Blog](https://codewithandrea.com/articles/flutter-firebase-multiple-flavors-flutterfire-cli/).
:::
