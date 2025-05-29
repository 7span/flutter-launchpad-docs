---
sidebar_position: 1
--- 

# Accessing Assets 📷

If you're used to adding assets in raw string format in Flutter, then this section is for you. 😉 

- We're using the [flutter_gen](https://pub.dev/packages/flutter_gen) package for utilizing code generation for our assets. 
The code that you used to write like this : 

```
Image.asset("assets/demo.png")
```

Will be replaced like this :

```
Assets.images.demo.image()
```

To use assets like the code above, follow the steps:

1. Add the assets in the assets folder in the **app_ui** package. 🤷

2. Run the build runner command: `melos run asset-gen`

3. Now you can use assets in the Flutter Launchpad project as shown.
