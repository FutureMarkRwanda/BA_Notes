# **Learning Outcome 2: Execute a Test**

### 📘 Learning Hours: 20

---

## 📌 Objective

By the end of this section, learners will be able to:
- Gather software test requirements based on principles and methodologies.
- Document inception reports with clear scope and objectives.
- Develop and execute test cases for functional and non-functional testing.
- Plan and schedule test execution effectively.

---

## 1. **Gathering Test Requirements**

### 1.1 Definition
Identifying stakeholder needs and software specifications to define test scope.

### 1.2 Example: Requirement Analysis
- **Stakeholder Need**: Ensure login page handles 1000 users.
- **Test Requirement**: Test login performance under load.

---

## 2. **Inception Report Analysis**

### 2.1 Definition
Documenting project scope, objectives, and quality assurance (QA) practices.

### 2.2 Example: Inception Report
```markdown
# Inception Report
- **Scope**: Test user authentication module.
- **Objectives**: Verify security and performance.
- **QA Metrics**: Response time < 2s, 99% uptime.
```

---

## 3. **Developing Test Cases**

### 3.1 Definition
Creating test cases based on requirements, using design techniques like boundary value analysis.

### 3.2 Example: Test Case Template
```markdown
**Test Case ID**: TC001
**Description**: Verify user login with valid credentials.
**Steps**:
1. Navigate to login page.
2. Enter valid username and password.
3. Click "Login".
**Expected Result**: User is redirected to dashboard.
```

### 3.3 Test Types
| Type             | Description                              |
|------------------|------------------------------------------|
| Functional       | Tests features (e.g., login works)       |
| Non-Functional   | Tests performance, security, usability   |

---

## 4. **Executing Test Cases**

### 4.1 Definition
Running tests in a controlled environment, including regression and performance testing.

### 4.2 Example: Test Execution in JUnit
```java
@Test
public void testLogin() {
  assertTrue(authService.login("user", "pass123"));
}
```

---

## ✅ Summary Table
| Concept               | Description                              | Example                        |
|-----------------------|------------------------------------------|--------------------------------|
| Test Requirements     | Stakeholder and software needs           | Login performance test         |
| Test Cases            | Structured test scenarios                | Login test case template       |
| Test Execution        | Running tests in environment             | JUnit login test               |

---

## 📚 Practice Exercises
1. Write a test case for a shopping cart’s “Add to Cart” feature.
2. Create an inception report for testing a mobile app’s payment module.
3. Execute a performance test for a web app using a tool like JMeter.