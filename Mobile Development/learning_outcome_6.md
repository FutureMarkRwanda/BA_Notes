# **Learning Outcome 6: Maintain the Mobile App**

### 📘 Learning Hours: 5

---

## 📌 Objective

By the end of this section, learners will be able to:
- Monitor app performance using tools like Prometheus.
- Secure the app with static code analysis and security testing.
- Update the app based on performance and user feedback [cite: 182].

---

## 1. **Monitoring App Performance**

### 1.1 Definition
Tracking metrics like response time and crash rates to ensure app reliability [cite: 182].

### 1.2 Example: Prometheus Monitoring
```yaml
scrape_configs:
  - job_name: 'realestatepro'
    static_configs:
      - targets: ['localhost:9090']
```

---

## 2. **Securing the Mobile App**

### 2.1 Definition
Using tools to identify vulnerabilities and ensure secure coding practices [cite: 183].

### 2.2 Example: Static Code Analysis
```bash
npm install eslint --save-dev
npx eslint src/
```

---

## 3. **Updating the Mobile App**

### 3.1 Definition
Releasing updates to fix bugs or add features based on feedback [cite: 183].

### 3.2 Example: App Update
```bash
# Update version in package.json
npm version patch
npx react-native run-android --variant=release
```

---

## ✅ Summary Table
| Concept               | Description                              | Example                        |
|-----------------------|------------------------------------------|--------------------------------|
| Performance Monitoring| Tracking app metrics                     | Prometheus configuration       |
| Security              | Ensuring secure code                     | ESLint static analysis         |
| Updates               | Releasing bug fixes/features             | Patch version update           |

---

## 📚 Practice Exercises
1. Set up Prometheus to monitor RealEstatePro’s API response time [cite: 182].
2. Run a static code analysis on a React Native component using ESLint [cite: 183].
3. Create an update plan for adding a new filter feature to the property list [cite: 183].