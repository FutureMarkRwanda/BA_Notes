# **Learning Outcome 1: Analyze Mobile App Requirements**

### 📘 Learning Hours: 10

---

## 📌 Objective

By the end of this section, learners will be able to:
- Understand mobile application concepts and types.
- Define cross-platform development and its frameworks (React Native, Flutter, Swift).
- Configure a development environment for React Native.
- Analyze requirements for a cross-platform mobile app like RealEstatePro.

---

## 1. **Mobile Application Concepts**

### 1.1 Definition
Mobile applications are software designed for mobile devices, categorized as native, web, or cross-platform apps [cite: 70].

### 1.2 Example: App Types
- **Native**: Built for specific platforms (e.g., Swift for iOS).
- **Web**: Browser-based apps.
- **Cross-Platform**: Single codebase for iOS and Android (e.g., React Native).

---

## 2. **Cross-Platform Development**

### 2.1 Definition
Cross-platform development uses frameworks to build apps compatible with multiple platforms [cite: 74].

### 2.2 Example: Framework Comparison
| Framework   | Language        | Use Case                     |
|-------------|-----------------|------------------------------|
| React Native| JavaScript      | RealEstatePro app            |
| Flutter     | Dart            | Rapid UI development         |
| Swift       | Swift           | iOS-specific apps            |

---

## 3. **React Native Introduction**

### 3.1 Definition
React Native is a framework for building cross-platform mobile apps using JavaScript and React [cite: 78].

### 3.2 Example: React Native Setup
```bash
npx react-native init RealEstatePro
npm install
```

---

## 4. **Development Environment Configuration**

### 4.1 Definition
Setting up tools like Visual Studio Code, Android Studio, and Xcode for development [cite: 99].

### 4.2 Example: Environment Setup
```bash
# Install Node.js and React Native CLI
brew install node
npm install -g react-native-cli
# Configure Android Studio
sdkmanager "platform-tools" "platforms;android-30"
```

---

## ✅ Summary Table
| Concept                  | Description                              | Example                        |
|--------------------------|------------------------------------------|--------------------------------|
| Mobile App Types         | Native, web, cross-platform              | React Native for cross-platform|
| Cross-Platform Frameworks| Tools for multi-platform apps            | React Native vs. Flutter       |
| Development Environment   | Configuring tools for coding              | Node.js and Android Studio setup|

---

## 📚 Practice Exercises
1. Compare the advantages of React Native vs. Flutter for RealEstatePro.
2. Set up a React Native development environment on your computer.
3. Draft a requirements document for the RealEstatePro app, listing features for admin, client, and agent roles [cite: 186].