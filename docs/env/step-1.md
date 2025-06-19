---
sidebar: 1
---

# Step 1

We're using envied package for the environment variables since it encrypts every key value inside your .env files.

By default, the Dart side of the environment files will be already given for your Base API URL and environment name. But you will need to create the .env files in order to utilize it in your Flutter App.

:::tip
- .env files will be generated while setting up Dashing-Kit through the command sh scripts/setup.sh.
- You can skip the 1st step in this case.
:::

To configure environment variables inside your Flutter project, Follow the steps below:

Create 2 files in app_core package name it like this:
- `.env.dev`
- `.env.prod`

Next, Add this 2 variables inside both env files like this:

```jsx title=".env.dev"
BASE_API_URL=YOUR API URL
ENV=Development
```

:::danger
- ENV key for .env.dev will be Development but it will be Production for .env.prod.
- Don't commit your .env file to a (public/private) repository.
:::

Now run the Flutter Build Runner command in order to generate your encrypted environment variables. dart run build_runner build.