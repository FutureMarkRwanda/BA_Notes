# Learning Outcome 5: Publish the Mobile App

This section covers the process of preparing, documenting, and publishing a cross-platform mobile application to the Google Play Store and Apple App Store. It emphasizes practical steps using React Native, with direct application to the deployment of the **RealEstatePro** project.

---

## 1. Preparing the App for Stores

### App Icon, Splash Screen, App Name, Screenshots, Descriptions

**App Icon**

* Represents the application visually on devices and in stores.
* Must meet platform requirements:

  * iOS: 1024×1024 px
  * Android: 512×512 px
* Implementation:

  * Android: `android/app/src/main/res/mipmap`
  * iOS: `Images.xcassets` in Xcode

**Splash Screen**

* Shown during app loading to reinforce brand identity.
* Should be simple and fast-loading.
* Implementation:

  * Android: `android/app/src/main/res/drawable`
  * iOS: `LaunchScreen.storyboard` or use `react-native-splash-screen`

**App Name**

* Must be unique, memorable, and compliant with store rules (e.g., ≤30 characters).
* Updated in:

  * `app.json` (Expo)
  * `AndroidManifest.xml` and Xcode project settings (React Native CLI)

**Screenshots**

* Highlight key features of the app (e.g., listings, dashboards).
* Must meet platform requirements for resolution and device type.

**Descriptions**

* Clear, keyword-rich text emphasizing value and features.
* Store limits: up to 4000 characters.

**RealEstatePro Example:**

* Icon with a house and key.
* Splash screen with RealEstatePro logo.
* Name: “RealEstatePro”
* Description: “RealEstatePro simplifies property management with secure login, rich listings, and easy CRUD operations.”

---

### App Store Optimization (ASO)

**Purpose:**
Improve visibility, discoverability, and download rates.

**Strategies:**

* Use relevant keywords in name, subtitle, and description.
* Translate metadata for multilingual markets.
* Use high-quality visuals and promotional content.
* Encourage and respond to reviews.

**Tools:**
App Annie, Sensor Tower

**RealEstatePro Example:**

* Keywords: “real estate app,” “Kigali properties,” “property rental”
* Localized content in English and Kinyarwanda


### Permissions and Store Guidelines

**Permissions**

* Declare only necessary permissions:

  * Camera (for photos)
  * Storage (for saving images/data)
* Justify use with user-friendly prompts.

**Google Play Guidelines**

* Follow Google Play policies:

  * No misleading content
  * Privacy policy required
  * GDPR and data safety section compliance

**Apple App Store Guidelines**

* Follow Human Interface Guidelines for UI/UX
* Submit data usage disclosures
* Include a valid privacy policy

**RealEstatePro Example:**

* Permissions: Camera and storage (for property photos)
* Privacy policy uploaded to both stores

---

## 2. Documentation

### User Guides and FAQs

**User Guides**

* Role-based documentation (admin, client, agent)
* Examples: “How to add a property,” “How to create a wishlist”

**FAQs**

* Answers to common questions
* Structured by user role or functionality

**Implementation:**

* In-app Help screen (`<ScrollView>` component)
* Web-based or embedded HTML/Markdown

**RealEstatePro Example:**

* In-app Help screen showing FAQs:

  * “How can I update my listing?”
  * “What image formats are accepted?”

---

### Localization and Internationalization

**Localization**

* Translate interface, content, and documentation into target languages.
* Use tools like `react-native-localize` and `i18n-js`.

**Internationalization**

* Support different:

  * Languages
  * Currencies (e.g., RWF, USD)
  * Date formats

**RealEstatePro Example:**

* Localize app content into Kinyarwanda and English.
* Display prices as “RWF 500,000” or “\$500” depending on region.

---

## 3. Publishing

### Code Signing and Provisioning Profiles

**Code Signing**

* Digitally signs the app to validate the publisher.

| Platform | Method                                                                                |
| -------- | ------------------------------------------------------------------------------------- |
| Android  | Generate a keystore via `keytool`; configure in `build.gradle`                        |
| iOS      | Use Apple Developer portal to generate signing certificates and provisioning profiles |

**Provisioning Profiles (iOS)**

* Link the app to a developer account and devices.
* Used during submission to App Store.

**RealEstatePro Example:**

* Android: Generate keystore for AAB
* iOS: Create provisioning profile for submission

---

### Build Tools and Release Management

**Build Tools**

* **Android:**

  * Release build: `./gradlew bundleRelease`
  * Output: `.aab` or `.apk` for Google Play

* **iOS:**

  * Use Xcode to archive and export `.ipa`
  * Submit via Transporter or App Store Connect

* **Automation Tools:**
  Fastlane for automating build, versioning, and upload workflows

**Release Management**

* Manage version numbers in `app.json` or `build.gradle`
* Test on emulators and real devices
* Submit using Google Play Console and App Store Connect
* Monitor crash reports using Firebase Crashlytics

**RealEstatePro Example:**

* Use Fastlane to automate iOS and Android builds
* Submit version 1.0.0 with release notes and store assets

---

## Summary of Key Concepts

| Area                 | Focus                                                                      |
| -------------------- | -------------------------------------------------------------------------- |
| Preparing for Stores | Icons, splash screens, metadata, and ASO improve visibility and branding   |
| Documentation        | Guides and multilingual support enhance user accessibility                 |
| Publishing Process   | Code signing, build tools, and release management ensure smooth deployment |

