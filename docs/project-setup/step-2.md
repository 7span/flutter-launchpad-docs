---
sidebar_position: 2
---

# Step 2

## Run setup scripts

- Run this command in the terminal to ensure an updated project environment.

```
sh scripts/check_environment_configuration.sh
```

- Next run this command in the terminal for initial project set-up. 

```
sh scripts/init.sh  
```

It will setup following things : 

- Environment Configuration (adds .env files)
- Assets, Locale and Routing Configurations
- Git Hooks
- Initialises mason_cli, mason and bricks
- Configures mason.yaml

