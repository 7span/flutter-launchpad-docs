---
sidebar: 1
---

# Deep Linking in Flutter (Web + Android + iOS) 📱 

Here’s a complete documentation guide for implementing Deep Linking in Flutter with Web, Android, and iOS, including file hosting, platform configuration, and Flutter-side setup using auto_route.

### Hosting Required Files 🌐 

#### ✅ For Android

- Host the following file on your domain: https://abc.com/.well-known/assetlinks.json
- Generate it using the official Asset Link Generator: [Asset Links Generator](https://developers.google.com/digital-asset-links/tools/generator)

```jsx title="Example JSON structure"
[
  {
    "relation": ["delegate_permission/common.handle_all_urls"],
    "target": {
      "namespace": "android_app",
      "package_name": "com.example.app",
      "sha256_cert_fingerprints": ["YOUR_APP_SHA256_FINGERPRINT"]
    }
  }
]
```

- Add the following in AndroidManifest.xml:

```jsx title="Inside <application> tag:"
<meta-data
    android:name="flutter_deeplinking_enabled"
    android:value="true" />
```

```jsx title="Add intent-filter inside <activity> tag:"
<intent-filter android:autoVerify="true">
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <data android:scheme="https" android:host="abc.com" />
</intent-filter>
```

### For iOS 🍏 

Create and host apple-app-site-association JSON file

This file uses the JSON format. Don't include the .json file extension when you save this file. Per [Apple's documentation](https://developer.apple.com/documentation/xcode/supporting-associated-domains), this file should resemble the following content.


https://abc.com/.well-known/apple-app-site-association
Open Xcode > Your Project Target > Signing & Capabilities > Add Associated Domains:

![guide](/img/guide.png)

![guide_2](/img/guide_2.png)

/// TODO : 2 image 


```jsx title="Example JSON structure:"
{
  "applinks": {
    "apps": [],
    "details": [
      {
        "appID": "TEAM_ID.bundle.identifier",
        "paths": ["/reset-password/*"]
      }
    ]
  }
}
```

1. Set one value in the appIDs array to team_id.bundle_id.
2. Set the paths array to ["*"]. The paths array specifies the allowed universal links. Using the asterisk, * redirects every path to the Flutter app. If needed, change the paths array value to a setting more appropriate to your app.
3. Host the file at a URL that resembles the following structure.
_webdomain_/.well-known/apple-app-site-association
4. Verify that your browser can access this file.

- For more Refer to the Flutter documentation 🔗 [Set up Universal Links in Flutter](https://docs.flutter.dev/cookbook/navigation/set-up-universal-links)

1. In Info.plist, add:

```jsx title="In Info.plist"
<key>FlutterDeepLinkingEnabled</key>
<true/>
```

### 🚀 Flutter Setup with auto_route

#### 1. Define the Route

If the deep link is like:
```
 https://abc.com/reset-password/abc123?email=user@example.com
```

Set it up in your router:

```
AutoRoute(
  path: '/reset-password/:token',
  page: ResetPasswordRoute.page,
),
```

#### 2. Use Path & Query Parameters in Your Page

```dart
@RoutePage()
class ResetPasswordPage extends StatelessWidget {
  final String? token;
  final String? email;

  const ResetPasswordPage({
    @PathParam('token') this.token,
    @QueryParam('email') this.email,
    super.key,
  });

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Text('Token: $token, Email: $email'),
    );
  }
}
```

#### 3. Enable Deep Linking in MaterialApp.router

```dart
MaterialApp.router(
  routerConfig: getIt<AppRouter>().config(
    includePrefixMatches: true,
    deepLinkBuilder: (deepLink) {
      debugPrint('DeepLink received: ${deepLink.path}');
      return deepLink;
    },
  ),
);
```

#### Testing Deep Links 🧪

▶️ Android (using adb from macOS Terminal)

```
adb shell 'am start -a android.intent.action.VIEW -c android.intent.category.BROWSABLE -d "https://abc.com/reset-password/abc123?email=user@example.com"'
```




