---
sidebar_position: 1
--- 

# Accessing Colors And TextStyles 🎨

- If you look at the extensions.dart file, you will be able to see extensions related to accessing colors and textstyles.
- In the DashingKit, we follow material conventions. So to use any color, you can use **context.colorscheme** like this:

```
Container(color:context.colorScheme.primary)
```

- Use **AppText** instead of Text widget to utilise typography.

```
AppText.medium(
 text:context.t.login,
 color: context.colorScheme.primary,
),
```

- Same way, You can use TextStyles using `context.textTheme`.

```
RichText(
  text: TextSpan(
    text: context.t.login,
    Style: context.textTheme.medium,
    )
)
```

- If you want to change/add any Colors or TextStyles, you can configure it from `colors.dart` and `typography.dart` respectively.
