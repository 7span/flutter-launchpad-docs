---
sidebar : 1
---

 # App branding and configuration

- Dashing-Kit provides a single command to change application name, application logo and application package name all together. 😉
- For this, run the following command.

```
sh scripts/project_setup.sh
```

:::danger
- If you want to change application logo make sure that you've added **.png** file in the following path : **packages/app_ui/assets/images/logo.png**
- The name should be **logo.png** only.
:::

- First you will be asked for an application name update.

### 1. Change App Name :  
When prompted, type y and enter the new app name to update it. ✅

![app-brand](/img/app-brand/app-brand-1.png)

- Next you will be asked to change the application package name.

### 2. Change Package Name : 
When prompted, type y and enter the new package name (e.g., com.abc.xyz) to update it for both Android and iOS. ✅

![app-brand](/img/app-brand/app-brand-2.png)

- Next you will be asked if you want to change the application logo.

### 3. Change App Logo : 
When prompted, type y, ensure the logo path is set to packages/app_ui/assets/images/logo.png, and the script will generate new launcher icons. ✅

![app-brand](/img/app-brand/app-brand-3.png)

And Voila you have successfully updated the app logo , app name and package name. 🎉

![app-brand](/img/app-brand/app-brand-4.png)

:::danger
- You will get an alert about re-configure your firebase project and updating the google-services.json file once you change the package name as Dashing-Kit provided default Firebase configuration will not work now.
- To re-configure Firebase follow the previos step.
:::

![app-brand](/img/app-brand/app-brand-5.png)
