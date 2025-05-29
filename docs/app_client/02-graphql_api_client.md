---
sidebar : 2
---

# GraphQL Client

- Uses **GraphQL** to connect to remote data sources.
- Handles API calls using a clean, functional approach via `fpdart`.

### Key Features

- **Initialization** with `init()`:
  - Configurable caching
  - Setup with base URL

- **Token Management**:
  - Dynamically set authorization tokens using `setAuthorizationToken`

- **Single Entry Point**:
  - `request()` handles all query/mutation calls
  - Accepts `.graphql` file path and optional variables

### Utilities

| Function               | Purpose                                               |
|------------------------|-------------------------------------------------------|
| `readGraphQLFile`      | Reads `.graphql` files from Flutter asset bundle      |
| `doApiCall`            | Executes GraphQL query/mutation based on `RequestType`|
| `validateResponse`     | Validates GraphQL response for exceptions             |
| `getResponseData`      | Extracts and returns the response payload             |

---

🔁 **Unified. Functional. Flexible.**

> API setup made effortless — with `app_client`.
