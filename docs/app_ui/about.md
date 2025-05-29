---
sidebar : 1
---

# app_ui 📦

The `app_ui` package is structured using the **Atomic Design Pattern** and includes:

- 🎨 App Themes  
- 🔤 Fonts  
- 📁 Assets Storage  
- 🧩 Common Widgets  
- 🛠️ Related Generated Files  

---

### Spacing 🛰️ ( Atom level )

- In this Flutter Starter Kit, you won't need to directly use SizedBox for spacing, because you'll have a better way to do it 😉 In the `spacing.dart` file.
- You will be able to configure the horizontal and vertical spacing parameters. 
- You can use HSpace or VSpace with their respective named constructors for adding empty space.
- This will ensure that whenever the user wants to change the spacing throughout the app, they will be able to do so by modifying just this class.

Thus instead of writing:

```
const SizedBox(height: 8)
```

You can write:

```
VSpace.xsmall()
```

:::info 
Other atom level classes
AppBorderRadius, Insets, AppText, AppLoadingIndicator
:::

### Accessing Buttons 🔵 ( Molecule Level )

- In the Flutter Starter Kit, There's file named app_button.dart that includes all the types and variations of the Buttons that you'll need in the entire App.
- You can go into that file and configure the buttons as per your App's design.

Example of using a button:

```
AppButton(
   text: context.t.login,
   onPressed:(){},
   isExpanded: true,
   isEnabled: false,
)
```

:::info
Other molecule level widgets
CustomAppBar, AppDropdownWidget , AppTextField, AppNetworkImage,
:::

:::tip
Animated widgets like AnimatedGestureDetector and SlideAndFadeAnimation are also included.
:::
