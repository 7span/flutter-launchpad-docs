---
sidebar : 1
---

# app_transalations 📦

app_translation package manages locale in application.

- You define a key-value pair for texts inside the application in each language's `.json` file.

### Implementation : 

- We are using a [**slang**](https://pub.dev/packages/slang) package for localization.
- Localization is configured by default in the Flutter Launchpad.
- You just need to add the key-value pair of the localization keys inside app_translations package.

Add a key-value pair like this in the `i18n` folder:

```
{
   "login": "Login Screen"
}
```

After you add the key-value pairs, run the command below to generate the corresponding code:

```
melos run locale-gen
```

Now you can use the key in the Flutter Launchpad project like this:

```
Text(context.t.login)
```

:::tip
You can learn more about the naming conventions of the localization keys by this [article](https://phrase.com/blog/posts/ruby-lessons-learned-naming-and-managing-rails-i18n-keys/)
:::

