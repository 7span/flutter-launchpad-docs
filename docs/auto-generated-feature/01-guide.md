---
sidebar : 1
---

# Guide

Yes you read right 😉

- You can generate new features with crud operation integrated with pagination just with a single command. (Thanks to mason 😁)

:::warning
- Before jumping into generating features, make sure you have run the **init.sh** script at-least once to ensure **mason_cli activation and brick configuration**.
:::

- Just run the following command.

```
mason make feature
```

- Next it will ask you the feature name for which you want to generate a module.

```
mason make feature
? What is the feature name? (new_feature) Ticket
```

- Hit enter after providing the feature name and YAAYYY the feature is ready at path **apps/app_core/lib/module** . 
