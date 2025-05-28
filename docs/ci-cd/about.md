---
sidebar: 1
---

# Pre-Integrated CI/CD WorkFlow 

Flutter Boilerplate provides pre-integrated CI/CD work with the following configurations.

1. Triggers on every push to **main** and **development** branches
2. Sets up Java and Flutter environment on GitHub-hosted macOS runner.
3. Creates secret files `.env.dev` , `.env.staging` and `.env.prod` for environment configuration.
4. Runs **melos** to bootstrap packages and execute code generation commands.
5. Builds the Android **production** APK using flavor-specific entry points.
6. Uploads the generated .apk artifact for easy download from the GitHub Actions tab.

:::warning
- We have integrated GitHub CI/CD for **Android** as of now.
- For step by step configuration of GitHub CI/CD in Android and iOS, follow this [**guide**](https://colorful-dinosaur-b59.notion.site/CI-CD-in-Flutter-1a6d70f4b3fc80459deefbda2fb0818d).
:::

:::danger
- Make sure you have added environment secrets into GitHub secrets that match the name in the `main.yaml` file of the **.github folder**.
:::