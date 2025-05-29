---
sidebar : 1
---

# app_subscription 📦

Flutter Starter Kit includes the app_subscription package.

### Implementation Of Product Purchase Flow

- Once the application opens, the handleSubscription method is called to initialize the PurchaseDetails stream, along with completing any pending purchases.
- You can call this function in the **Splash Screen**.

```
// Handles Subscription Initialization

Future<void> handleSubscription() async {
  customInAppPurchase = CustomInAppPurchase();
  customInAppPurchase.init();
  await customInAppPurchase.completePendingPurchases();
  await navigate();
}
```

- Now when the user lands on the PayWall/Subscription screen we will first fetch all the plans available in Google Play Console by calling **getPlans** method.

```
..getPlans(
    context,
    SubscriptionUtils.subscriptionProductId,
);
```

- Based on plans fetched, we can show the UI related to card details.
- Now when a user buys the `consumable products` we will call the **purchaseCredit** method from SubscriptionCubit and for `non-consumable products` (Subscription) **purchaseSubscription** method .

```
// Purchase Consumable Product
onTap: () async {
  await context.read<SubscriptionCubit>().purchaseCredit(
    context,
    SubscriptionUtils.subscriptionProductId[0],
  );
},
// Purchase Non-Consumable product / Subscription 
onTap: () async {
  await context.read<SubscriptionCubit>().purchaseSubscription(
    context,
    'yearly_subscription',
  );
}
```

- Implement BlocListener to listen to purchase status and show messages accordingly.

```
listener: (context, state) {
    if (state.status == SubscriptionStateStatus.purchaseSuccess) {
      showAppSnackbar(context, 'Purchase Successfully');
              context.read<SubscriptionCubit>().getAndSetActivePlanOfUser();
    }
    flog('status in listen of subscription: ${state.status}');
  },
```

:::danger
Do not forget to override the back gesture to prevent the user from closing the screen while purchasing is ongoing.
:::

- For example, leveraging BackButtonListener from `auto_route` we can showSnackBar to prevent users from disposing of the screen.

```
onBackButtonPressed: () async {
  if (context.read<SubscriptionCubit>().state.status ==
      SubscriptionStateStatus.purchaseLoading) {
    showAppSnackbar(
      context,
      'Please wait until we verify your subscription',
    );
    return true;
  } else {
    return false;
  }
}
```

:::tip
- For diving in-app purchase integration for apple app store and goole play store follow this [guide](https://in-app-purchase-doc.vercel.app/).
:::
