---
sidebar_position: 1
--- 

# Routing ⤴️

We're using the [auto_route](https://pub.dev/packages/auto_route) package for the routing. They help us to use the newer Navigator 2.0 API while keeping the learning curve as low as possible.

- The boilerplate comes with the routing setup out of the box. Thus, this guide will help you to create your own routes.

### 1. Annotating the screen

- Let's say you're creating a HomeScreen widget and you want to add that in your routes. The code should look something like this:

```jsx title="home_screen.dart "

class HomeScreen extends StatelessWidget {
    const HomeScreen({super.key});

    @override
    Widget build(BuildContext context) {
        return ...your code;
    }
}
```
1. Import the Auto Route package into your file:

```
import 'package:auto_route/auto_route.dart';
```

2. Annotate your Widget by `@RoutePage()` like this:

```
@RoutePage()
class HomeScreen extends StatelessWidget {
    const HomeScreen({super.key});

    @override
    Widget build(BuildContext context) {
        return ...your code;
    }
}
```

:::tip
Make sure that your Screen's name is either ending with Page or Screen. ( E.g. HomeScreen, HomePage)
:::

### 2. Adding the route in app_router.dart

1. Add your route in `app_router.dart` like this:

```jsx title="app_router.dart"
@AutoRouterConfig(replaceInRouteName: 'Page|Screen,Route')
class AppRouter extends RootStackRouter {
  @override
  List<AutoRoute> get routes => [
        AutoRoute(
          initial: true,
          page: SplashRoute.page,
          guards: [
            AuthGuard(),
          ],
        ),
        AutoRoute(page: HomeRoute.page),
      ];
}
```

2. Finally, run the build_runner command to generate the routes.

```
melos run build-runner
```

:::tip
To learn more about auto_route refer to articles by Cavin Macwan on [medium](https://medium.com/@CavinMac/list/auto-route-in-flutter-105bbe608e12).
:::
