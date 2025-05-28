---
sidebar: 3
---

# Step 3

### Bonus

If you ever have to render a widget based on the environment, then you can do it like this:

```
/// Here you can take any env, for this demo we're taking 

`development`
if (AppConfig.environment==Env.development) {
   ....
 }
```

:::danger
If you're changing the content of the .env files after you configure them, then make sure to run this command:
`melos run build-runner`
:::