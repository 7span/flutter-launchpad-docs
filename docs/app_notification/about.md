---
sidebar : 1
---

# app_notification_service 📦

### OneSignal Notification Integration

- We’ve implemented the entire notification flow — from **handling permissions** to capturing the **player ID**.

- app_notification_service package has OneSignalService class that implements abstract interface class **NotificationServiceInterface** to provide methods to fetch notifications id and to handle notification permission.

- **NotificationCubit** syncs `PlayerId` with the backend and stores it in local storage via `Hive`.
Integrated at app entry point for seamless setup.
