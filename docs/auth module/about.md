---
sidebar : 1
---

# Authentication/auth Module 🔐

The authentication(auth) module provides a whole user authentication flow with a mock api.

😉 Simply change baseUrl & api end-points and user authentication is ready.

### Implemented features :

1. **Request & Response Models** : Predefined authentication models for seamless API integration.
2. **User Model (Hive Storage)** – Store & manage user data locally with Hive.
3. **Auth Repository** – Well-structured login, sign-up, and logout flows.
4. **Secure Routing (Auth Guard)** – Restrict access for unauthenticated users.
5. **Change Password Support** – Enable users to update credentials securely.
6. **Delete Account API** – Handle account removal requests effortlessly.
7. **Hive Services** – CRUD operations for user data in local storage.

### Social Signing (Sign in with Google and Apple)

#### 🔐 Google Sign-In Auth Helper : GoogleAuthHelper

- Complete wrapper around Google Sign-In + FirebaseAuth
for a clean and plug-and-play experience.
- Handles sign-in, sign-out, and current user fetch.
- Built-in callbacks for success and error handling.
- Auto-creates AuthRequestModel with playerId support.

#### 🍎 Apple Sign-In Auth Helper : AppleAuthHelper

- Uses sign_in_with_apple for native integration.
- Returns ready-to-use AuthRequestModel.
- Optional callback for success/error flows.
- playerId placeholder for OneSignal sync.
- Built with platform scopes: email & fullName.

:::warning
As we all know, in Sign in with Apple, when a user chooses to hide their email, Apple automatically redirects emails to their original email address.

However, to enable this functionality, some setup is required. You can follow this [**guide**](https://developer.apple.com/help/account/capabilities/configure-private-email-relay-service/).
:::
