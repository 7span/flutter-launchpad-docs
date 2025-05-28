---
sidebar: 2
---

# Step 2

### Adding your own environment variables:

Adding your own environment variables is as easy as defining it. To add your own environment variables, follow the steps below:

1. Add your variables in the `.env` files. Let's say you want to add PATH variable for only `.env.dev`, then first add it into .env.dev file like this:

```jsx title=".env.dev"

BASE_API_URL=https://jsonplaceholder.typicode.com/
ENV=Development
PATH=Home
```
2. Now, Go to `app_config.dart` inside the ** lib -> app -> config**. There will be an abstract class called **EnvDev**. Add PATH variable like this:

```jsx title="app_config.dart"

@Envied(path: '.env.dev')
abstract class EnvDev {
 @EnviedField(varName: 'BASE_API_URL', obfuscate: true)
 static final String ENV_BASE_API_URL = _EnvDev.ENV_BASE_API_URL;
 @EnviedField(varName: 'ENV', obfuscate: true)
 static final String ENV_NAME = _EnvDev.ENV_NAME;
 @EnviedField(varName: 'PATH', obfuscate: true)
 static final String ENV_PATH = _EnvDev.ENV_PATH;
}
```

3. Now run the Flutter Build Runner command in order to generate your encrypted environment variables.

```
dart run build_runner build
```

4. The last step is to create the **getters** for the variable. You can look into the implementation of other getter variables inside the `app_config.dart` file in order to implement it.
