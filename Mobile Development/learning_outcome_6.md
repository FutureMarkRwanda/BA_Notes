# Learning Outcome 6: Maintain the Mobile App

This learning outcome emphasizes the ongoing maintenance of a mobile application after deployment, including performance monitoring, security, app updates, and full-lifecycle project execution. It is exemplified through the **RealEstatePro** project, where learners are required to maintain a role-based, cross-platform application that integrates both front-end and back-end systems.

---

## 1. Performance Monitoring

### Crash Reporting

* **Purpose:** Detect and log crashes for debugging and stability improvement.
* **Tools:** Firebase Crashlytics, Sentry.
* **RealEstatePro Example:** Use Crashlytics to monitor crashes during property form submissions or list browsing.

### Memory Profiling

* **Purpose:** Detect memory leaks and inefficient resource handling.
* **Tools:** Android Profiler (Android Studio), Xcode Instruments (iOS).
* **RealEstatePro Example:** Use profiling tools to analyze image memory usage in property components.

### Optimization

* **Purpose:** Improve performance and responsiveness.
* **Techniques:**

  * `useMemo`, `useCallback` to avoid re-renders.
  * Lazy loading for images (`react-native-fast-image`).
  * Cache property data using `AsyncStorage`.
* **RealEstatePro Example:** Optimize `FlatList` with memoized property data.

---

## 2. Security

### Code and Network Security

* **Practices:**

  * Use `.env` for API keys (`react-native-config`).
  * Enforce HTTPS and certificate pinning.
  * Sanitize backend responses.
* **RealEstatePro Example:** API keys secured in `.env`, HTTPS enforced for all API calls.

### Secure Storage of Auth Tokens

* **Storage Solutions:**

  * `AsyncStorage` (with encryption), `react-native-keychain`, Android Keystore.
* **RealEstatePro Example:** Secure JWT tokens for user sessions; clear on logout.

### Static Code Analysis and Audits

* **Tools:** ESLint (`eslint-plugin-security`), SonarQube, `npm audit`, Snyk.
* **RealEstatePro Example:** Use Snyk to detect vulnerable packages; ESLint to enforce secure coding.

---

## 3. App Updates

### Patch Management

* **Tools:** CodePush (for OTA JS updates), App Store & Google Play for native code changes.
* **RealEstatePro Example:** Push validation fixes using CodePush without re-submitting to stores.

### Bug Fixes & Feature Enhancements

* **RealEstatePro Example:**

  * Bug fix: property images not loading due to incorrect URLs.
  * Feature: allow agents to upload multiple images per listing.

### Version Control

* **Practices:** Git + GitHub/GitLab, GitFlow (feature, develop, main branches), semantic versioning.
* **RealEstatePro Example:** Use GitHub for managing features (`feature/property-filter`) and releases (`v1.0.1`).

---

## 4. Integrated Assessment Project: RealEstatePro App

### Project Overview

**Objective:** Build and maintain a cross-platform app for real estate listing and management with support for Admin, Client, and Agent Operator roles.

### Key Functional Requirements

* **CRUD Operations:** Properties with detailed attributes and media.
* **User Roles & Permissions:**

  * Admin: full access including agent management.
  * Client: browse, wishlist, submit purchase/rent orders.
  * Agent: add/update property listings.

### Authentication & Authorization

* **Firebase Auth + JWT**
* **RBAC Enforcement:** Role-based logic in both front-end UI and back-end API.

---

## 5. Tools Used in Maintenance and Development

| Category        | Tools/Technologies                                        |
| --------------- | --------------------------------------------------------- |
| **Core Stack**  | React Native, Expo, Firebase (Auth, Firestore), REST APIs |
| **IDE & Dev**   | VS Code, Android Studio, Xcode                            |
| **Design**      | Figma, Adobe XD                                           |
| **State Mgmt**  | Redux, Context API, AsyncStorage                          |
| **Forms**       | Formik, Yup for validation                                |
| **HTTP**        | Axios                                                     |
| **Testing**     | Jest, React Testing Library, Detox, Postman               |
| **CI/CD & VCS** | Git, GitHub, Bitbucket, GitLab, Fastlane, CodePush        |

---

## 6. Skills Developed

### UI/UX Design & Responsive Layouts

* Mockups designed in Figma/Adobe XD for all user roles.
* Responsive layouts implemented using Flexbox and `react-native-responsive-screen`.

### State & Form Management

* Redux and `useState` used for managing local/global state.
* Formik used for form creation, validation, and submission logic.

### Debugging, Testing & Deployment

* Tools: React Native Debugger, Chrome DevTools, Jest, Detox, Fastlane.
* RealEstatePro Example: E2E test for a client browsing and wishlisting properties.

---

## 7. Attitudes & Professional Practices

| Attitude                   | Description                                                          |
| -------------------------- | -------------------------------------------------------------------- |
| **Attention to Detail**    | UI consistency, thorough form validation, error handling             |
| **Problem-Solving**        | Debug platform-specific bugs, performance tuning, edge case handling |
| **Team Collaboration**     | Git-based collaboration, code reviews, shared documentation          |
| **Adaptability**           | Stay current with library updates (e.g., React Navigation v6)        |
| **User-Centered Thinking** | Implement features based on real user feedback and usability goals   |

---

## 8. RealEstatePro Implementation Examples

| Feature               | Implementation                                                                   |
| --------------------- | -------------------------------------------------------------------------------- |
| Property CRUD         | FlatList for rendering, Formik for forms, Axios for API calls                    |
| User Authentication   | Firebase Auth for login + JWT storage in AsyncStorage                            |
| Role-Based Navigation | React Navigation stack/tab logic customized by user role                         |
| State Normalization   | Redux store with property entities normalized by ID                              |
| API Testing           | Postman used to verify endpoints; tests written in Jest and Detox                |
| Localization          | `i18n-js` and `react-native-localize` for English/Kinyarwanda UI text            |
| Deployment            | Build scripts using Fastlane, OTA updates with CodePush, version control via Git |

---

## Summary: Key Takeaways

| Area                  | Highlights                                                                 |
| --------------------- | -------------------------------------------------------------------------- |
| **Maintenance**       | Crash monitoring, profiling, secure updates, token storage                 |
| **Security**          | HTTPS, RBAC, secure storage, code scanning, environment config             |
| **Project Execution** | Full lifecycle: design → develop → test → deploy → maintain                |
| **Tools Mastery**     | Effective use of React Native stack, Firebase, Figma, Git, CI/CD pipelines |
| **Team & Growth**     | Collaboration, documentation, adaptability, real-world professionalism     |
