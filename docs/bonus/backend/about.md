---
sidebar: 1
---

# Backend Integration Document 📘

#### 📍Purpose

This document outlines the API response structure and communication expectations between the backend and mobile teams. The goal is to maintain a consistent contract for both successful and error responses, as well as define the format for authentication APIs.

### ✅ Standard Success Response Format

- Every successful API response must follow the below structure:

```dart
{
  "message": "Operation successful",
  "data": {
    // actual payload here
  }
}
```

#### Keys Explained:

- **message** : A human-readable message for debugging or display.
- **data** : A JSON object or array containing the actual response payload.

#### 📌 Example:

```
{
  "message": "User profile fetched successfully",
  "data": {
    "id": 123,
    "name": "John Doe",
    "email": "john.doe@example.com"
  }
}
```

### ❌ Error Response Format

Every API failure (client or server-side) must follow this format:

```
{
  "message": "Invalid token",
  "error_code": "AUTH_401"
}
```

#### Keys Explained:

- **message**: Short message to display or log.
- **error_code**: (Optional but recommended) A unique error identifier to help in debugging or analytics.

#### 📌 Example:

```
{
  "message": "Email or password is incorrect",
  "error_code": "AUTH_001"
}
```

###  Authentication API Specification 🔐

This section outlines how the mobile team will interact with login, signup, or token refresh APIs.

#### 1. Login / Signup Request Format

```
{
  "email": "user@example.com",
  "password": "userPassword123",
  "device_type": "Android/iOS/Web"
  "notification_device_id": "hv283b"
}
```

- Optional fields (for signup):

```
{
  "name": "John Doe",
  "phone": "9876543210"
}
```
#### 2. Login / Signup Success Response

```
{
  "message": "Login successful",
  "data": {
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refresh_token": "8sdf9s8df9s8df9s8df...",
    "user": {
      "id": 1,
      "name": "John Doe",
      "email": "john.doe@example.com",
      "profile_image": "https://example.com/img/profile.jpg"
    }
  }
}
```

#### 3. Token Expiry or Invalid Token Response

```
{
   "message": "Access token expired",
   "error_code": "AUTH_401"
}
```

### Notes for Backend Developers 🧩

- Ensure consistent use of HTTP status codes (e.g., 200 for success, 400/401/500 for errors).
- Always send responses in the standard JSON format as described above.
- Timestamp fields should be in epoch format.

### Future-Proofing 🧪 

- Error codes can be extended to support localization or UI mapping.
- The authentication format may evolve to support OAuth2 or biometric flows in the future.
