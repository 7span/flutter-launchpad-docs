---
sidebar: 1
---

# App Development Prerequisites 🧱

This document outlines the required inputs and confirmations we need from the product manager or client before starting development. Ensuring these are addressed upfront helps reduce delays and miscommunication.

### 1. Product Requirements 🧾 

- Finalized feature list or user stories
- Prioritized MVP scope (Minimum Viable Product)
- Known business rules or logic
- Any non-functional requirements (e.g., offline mode, performance targets)

#### Questions for Product Manager / Owner 📋

- Are there any expected usage patterns or scalability concerns?
- Are there specific compliance or data handling rules we need to follow (e.g., GDPR)?

### 2. Design Inputs 🎨

- Access to Figma files or design system (Material 3 preferred)
- Defined brand assets (logos, colors, fonts)
- Approved UI prototypes or wireframes

### 3. Backend & API 🔗

- API documentation or access credentials (Bruno preferred)
- Swagger (Optional)
- Confirmed endpoints and expected responses
- WebSocket or push notification setup (if applicable)

#### Questions for Product Manager / Owner 📋 

- Will it be REST API or GraphQL?
- Will it follow the backend request/responses rules as per the documentation, or there will be any changes in it?
- How many environments will be there? 

### 4. Project Setup 🧱

- Initial repository setup (GitHub/GitLab/Bitbucket)
- CI/CD preferences (optional)

### 5. Tools & Integrations 🧰

- Analytics (e.g., Firebase Analytics, Mixpanel)
- Crash reporting (e.g., Sentry, Crashlytics)
- Third-party services (e.g., payment, maps, messaging)
- Translation/localization setup (if applicable)
- Firebase project credentials (if used) or access on PM & Developer’s Email Id
- Any SDK keys or service credentials needed

#### Questions for Product Manager / Owner 📋 

- Are there any required integrations that we need to plan for early (e.g., payment gateways, CRM tools)?
- Do you have existing subscriptions or accounts for third-party tools?
- What analytics metrics are most important to you for MVP and beyond?

### 6. App Store Deployment 📱

To publish on Google Play and Apple App Store, the following are required:

#### General 📤 
- App name
- Package name (Android) / bundle ID (iOS)
- App description, keywords, and screenshots
- App category (e.g., education, productivity)
- App privacy policy URL
- App Deletion URL

#### Google Play 🟢 
- Access to Google Play Console (admin or release manager)
- App icon (512x512) and feature graphic (1024x500)

#### Apple App Store 🍎
- Access to App Store Connect (admin or app manager role)
- Apple Developer Program enrolment (individual or organisation) ([Guide](https://support.spotme.com/hc/en-us/articles/360021425634-How-to-choose-the-type-of-Apple-account-I-need))
- Apple Team ID and App Store Connect Team Name
- App icon set and iOS-specific launch screen assets

