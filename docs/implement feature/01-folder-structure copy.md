---
sidebar : 1
---

# Create necessary folders 📁

1. Create a folder inside the lib/modules which is located in the app_core package. The name of the folder should be your feature name. Let's take an example of a home feature.
- Example: auth, home, profile, etc.

```
lib
└── modules
    └── home
```

2. Now, Create 4 folders like this:

```
lib
└── modules
   ├── home
   │   ├── bloc
   │   │   ├── home_event.dart
   │   │   ├── home_state.dart
   │   │   └── home_bloc.dart
   │   │── model
   │   │   └── home_model.dart
   │   ├── repository
   │   │   └── home_repository.dart
   │   ├── screen
   │   │   └── home_screen.dart
```

Where;

| **Folder Name 📂** | **Use-case 🔠** |
|--------------------|-----------------|
| **Home 🏠**         | Feature name |
| **bloc 🧱**         | Contains BLoC, Event, and States related to the feature |
| **model 🏪**        | Contains Dart model classes used for JSON conversion |
| **repository 🪣**   | Contains functions for API calling |
| **screen 📲**       | Contains UI of the feature |
