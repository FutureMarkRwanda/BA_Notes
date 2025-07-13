# Learning Outcome 7: Develop a Testing Strategy


## 🎯 Objective

By the end of this outcome, learners will be able to:

* Design a structured testing strategy for cross-platform mobile apps.
* Write unit tests for individual components using **Jest** and **React Testing Library**.
* Perform widget/UI tests to validate behavior across platforms.
* Conduct integration (end-to-end) tests using **Detox**.
* Apply testing best practices to maintain app reliability and user satisfaction.

---

## 1. Unit Testing

### 1.1 Definition

Unit testing focuses on verifying the behavior of individual, isolated units (e.g., components, functions) of the app.

> 🔹 *Tool:* Jest
> 🔹 *Scope:* Business logic, UI rendering, and prop handling within a single component
> 🔹 *RealEstatePro Context:* Test components like `PropertyCard`, `LoginForm`, `PropertyForm`

### 1.2 Example: Testing the Property Component

```jsx
import { render, screen } from '@testing-library/react-native';
import Property from './Property';

test('renders property details correctly', () => {
  render(<Property name="Villa" price={500000} />);
  expect(screen.getByText('Villa - $500,000')).toBeTruthy();
});
```

---

## 2. Widget Testing

### 2.1 Definition

Widget testing (UI testing) ensures that UI components such as buttons, inputs, and toggles behave as expected on real devices and emulators.

> 🔹 *Tool:* React Testing Library
> 🔹 *Focus:* Visual elements and interaction behavior (e.g., button clicks, input events)

### 2.2 Example: Testing Property Form Submission

```jsx
import { render, screen, fireEvent } from '@testing-library/react-native';
import PropertyForm from './PropertyForm';

test('submits property form', () => {
  const onSubmit = jest.fn();
  render(<PropertyForm onSubmit={onSubmit} />);
  fireEvent.changeText(screen.getByPlaceholderText('Property Name'), 'Apartment');
  fireEvent.press(screen.getByText('Submit'));
  expect(onSubmit).toHaveBeenCalledWith({ name: 'Apartment' });
});
```

---

## 3. Integration Testing

### 3.1 Definition

Integration testing validates complete user flows and the interaction between components, APIs, and navigation.

> 🔹 *Tool:* Detox
> 🔹 *Focus:* End-to-end (E2E) behavior across the app lifecycle
> 🔹 *RealEstatePro Example:* Test that a client can log in, browse properties, and add one to their wishlist.

### 3.2 Example: Detox E2E Property Flow

```js
describe('Property Flow', () => {
  beforeAll(async () => {
    await device.launchApp();
  });

  it('should add and display a property', async () => {
    await element(by.id('addPropertyButton')).tap();
    await element(by.id('nameInput')).typeText('Villa');
    await element(by.id('submitButton')).tap();
    await expect(element(by.text('Villa'))).toBeVisible();
  });
});
```

---

## 4. Testing Strategy for RealEstatePro

### 4.1 Definition

A **testing strategy** defines a structured plan combining unit, widget, and integration tests to validate the reliability, performance, and functionality of an app across platforms.

> 🔹 *Goal:* Achieve ≥80% code coverage and validate key user flows
> 🔹 *Scope:* Functional correctness, UI consistency, cross-role interaction integrity

### 4.2 RealEstatePro Testing Strategy Outline

```markdown
# RealEstatePro Testing Strategy

## Unit Tests
- Target: UI components like PropertyCard, LoginForm
- Tool: Jest
- Target coverage: 80%

## Widget Tests
- Test: Button presses, form inputs, navigations
- Tool: React Testing Library
- Run on: Android Emulator, iOS Simulator

## Integration Tests
- Flow: User login → Browse → Wishlist → Submit Order
- Tool: Detox
- Backend: Mock API responses

## Tools:
- Jest, React Testing Library, Detox, React Native Debugger
```

### 4.3 Testing Tools Summary

| Tool                      | Purpose                                      |
| ------------------------- | -------------------------------------------- |
| **Jest**                  | Unit testing of components and functions     |
| **React Testing Library** | Widget/UI testing of user interactions       |
| **Detox**                 | E2E testing for complete user journeys       |
| **React Native Debugger** | Debugging test failures and state inspection |

---

## Summary Table

| Concept              | Description                          | Example                                     |
| -------------------- | ------------------------------------ | ------------------------------------------- |
| **Unit Testing**     | Test single component functionality  | Test `PropertyCard` renders props correctly |
| **Widget Testing**   | Test UI element interactions         | Test `PropertyForm` submits data            |
| **Integration Test** | Test component and API interactions  | Detox test for property creation flow       |
| **Testing Strategy** | Combine all levels for full coverage | RealEstatePro testing plan using 3 tools    |

---

## Practice Exercises

1. **Unit Test:**
   Create a Jest unit test for a `LoginForm` component that validates rendering of input fields and submit button.

2. **Widget Test:**
   Write a React Testing Library test that ensures pressing a “Search” button navigates to the `SearchScreen`.

3. **Integration Test:**
   Using Detox, automate the process of a client logging in, browsing properties, adding one to the wishlist, and verifying the updated list.

---

## Key Takeaways

* A robust testing strategy improves app reliability, user experience, and maintainability.
* Use **unit tests** for logic validation, **widget tests** for UI interactions, and **integration tests** to verify complete workflows.
* Testing tools like Jest, React Testing Library, and Detox are critical in a cross-platform React Native environment.
* The RealEstatePro app requires a complete test coverage plan due to its role-based access and multi-step workflows.
