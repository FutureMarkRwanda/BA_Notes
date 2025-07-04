# **Learning Outcome 7: Develop a Testing Strategy**

### 📘 Learning Hours: 10

---

## 📌 Objective

By the end of this section, learners will be able to:
- Design a testing strategy for a cross-platform mobile application.
- Implement unit tests for individual components using Jest and React Testing Library.
- Conduct widget tests for UI elements in React Native.
- Perform integration tests to verify interactions between app components and APIs.
- Apply testing best practices to ensure the RealEstatePro app meets quality standards [cite: 160, 161, 162].

---

## 1. **Unit Testing**

### 1.1 Definition
Unit testing verifies the functionality of individual components (e.g., React Native components) in isolation [cite: 160].

### 1.2 Example: Unit Test for Property Component
```jsx
import { render, screen } from '@testing-library/react-native';
import Property from './Property';

test('renders property details correctly', () => {
  render(<Property name="Villa" price={500000} />);
  expect(screen.getByText('Villa - $500,000')).toBeTruthy();
});
```

---

## 2. **Widget Testing**

### 2.1 Definition
Widget testing ensures UI elements (e.g., buttons, text inputs) in React Native render and behave correctly across platforms [cite: 161].

### 2.2 Example: Widget Test for Property Form
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

## 3. **Integration Testing**

### 3.1 Definition
Integration testing verifies interactions between components, APIs, and external services in the app [cite: 162].

### 3.2 Example: Integration Test with Detox
```javascript
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

## 4. **Testing Strategy for RealEstatePro**

### 4.1 Definition
A testing strategy combines unit, widget, and integration tests to ensure app functionality, UI reliability, and system integration for cross-platform apps [cite: 160].

### 4.2 Example: Testing Strategy Outline
```markdown
# RealEstatePro Testing Strategy
- **Unit Tests**:
  - Test components (e.g., Property, PropertyForm) with Jest.
  - Coverage: 80% of codebase.
- **Widget Tests**:
  - Test UI interactions (e.g., button clicks, form inputs) with React Testing Library.
  - Platforms: iOS and Android emulators.
- **Integration Tests**:
  - Test end-to-end flows (e.g., add property, fetch properties) with Detox.
  - Validate API integration with mock responses.
- **Tools**: Jest, React Testing Library, Detox, React Native Debugger.
```

### 4.3 Testing Tools
| Tool                  | Purpose                              |
|-----------------------|--------------------------------------|
| Jest                  | Unit and widget testing              |
| React Testing Library | Testing UI component behavior        |
| Detox                 | End-to-end integration testing       |
| React Native Debugger | Debugging test failures              |

---

## ✅ Summary Table
| Concept               | Description                              | Example                        |
|-----------------------|------------------------------------------|--------------------------------|
| Unit Testing          | Testing individual components            | Jest test for Property component|
| Widget Testing        | Testing UI elements                      | Form submission test           |
| Integration Testing   | Testing component interactions           | Detox E2E property flow test   |
| Testing Strategy      | Comprehensive testing plan               | RealEstatePro testing outline  |

---

## 📚 Practice Exercises
1. Write a unit test for a login component using Jest and React Testing Library [cite: 160].
2. Create a widget test for a property search button to ensure it triggers the correct navigation [cite: 161].
3. Develop an integration test with Detox to verify the client’s ability to submit a wish list in RealEstatePro [cite: 162].