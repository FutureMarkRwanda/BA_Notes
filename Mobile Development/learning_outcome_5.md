# **Learning Outcome 5: Publish the Mobile App**

### 📘 Learning Hours: 5

---

## 📌 Objective

By the end of this section, learners will be able to:
- Prepare the app for publication (e.g., build, optimize).
- Document user references for the app.
- Publish the RealEstatePro app to iOS and Android stores [cite: 178].

---

## 1. **Preparing for Publication**

### 1.1 Definition
Optimizing the app (e.g., minifying code, configuring build settings) for release [cite: 178].

### 1.2 Example: Build for Android
```bash
cd RealEstatePro
npx react-native run-android --variant=release
```

---

## 2. **Documenting User References**

### 2.1 Definition
Creating guides for users (e.g., admin, client) to use the app [cite: 179].

### 2.2 Example: User Guide
```markdown
# RealEstatePro User Guide
- **Client**: Browse properties -> Tap property -> Submit wish list.
- **Admin**: Navigate to dashboard -> Manage properties -> Save changes.
```

---

## 3. **Publishing the App**

### 3.1 Definition
Uploading the app to Google Play Store and Apple App Store [cite: 178].

### 3.2 Example: Android Publishing
```plaintext
1. Generate signed APK in Android Studio.
2. Upload to Google Play Console.
3. Submit for review.
```

---

## ✅ Summary Table
| Concept               | Description                              | Example                        |
|-----------------------|------------------------------------------|--------------------------------|
| App Preparation       | Optimizing for release                   | Android release build          |
| User Documentation    | Guides for app usage                     | Client user guide              |
| Publishing            | Uploading to app stores                  | Google Play Console upload     |

---

## 📚 Practice Exercises
1. Generate a release build for RealEstatePro in Android Studio [cite: 178].
2. Write a user guide for the agent role’s property management tasks [cite: 179].
3. Outline steps to publish the app to the Apple App Store [cite: 178].