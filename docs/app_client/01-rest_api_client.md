---
sidebar : 1
---

# Rest Api Client

`app_client` package provides api call related set-up.

- RestApiClient class is used for connecting with remote data sources using Dio as an API Client.
- This class is responsible for making API requests and sending the response in case of success and error in case of API failure.
- Connects to remote data sources using **Dio**.
- Supports API request methods: `GET`, `POST`, `PUT`, `DELETE`, and `dynamic`.
- Centralizes error handling and token management.

### Key Features

- **Caching**  
  Optional caching with `DioCacheInterceptor` and `HiveCacheStore`.

- **Token Handling**  
  Automatically manages access and refresh tokens via `ApiTokensInterceptor`.

- **Logging**  
  API logs are beautified using `PrettyDioLogger`.

### Initialization

```dart
await restApiClient.init(
  isApiCacheEnabled: true,
  baseURL: 'https://your-api.com',
  refreshTokenEndpoint: '/auth/refresh',
  endPointsToEscapeHeaderToken: ['/auth/login'],
  onForceLogout: () => handleLogout(),
);