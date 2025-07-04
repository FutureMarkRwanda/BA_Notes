# **Learning Outcome 3: Develop Front End with React Native**

### 📘 Learning Hours: 30

---

## 📌 Objective

By the end of this section, learners will be able to:
- Apply React Native fundamentals (components, JSX).
- Implement UI navigation with React Navigation.
- Use React Native hooks and form handling (Formik, React Hook Form).
- Manage state with Redux or MobX.
- Perform unit tests with Jest and React Testing Library.

---

## 1. **React Native Fundamentals**

### 1.1 Definition
React Native uses components and JSX to build cross-platform UI [cite: 147].

### 1.2 Example: Property Component
```jsx
import React from 'react';
import { View, Text } from 'react-native';

const Property = ({ name, price }) => (
  <View>
    <Text>{name} - ${price}</Text>
  </View>
);
export default Property;
```

---

## 2. **UI Navigation**

### 2.1 Definition
Navigation enables seamless movement between app screens [cite: 150].

### 2.2 Example: React Navigation Setup
```jsx
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
const Stack = createStackNavigator();

const App = () => (
  <NavigationContainer>
    <Stack.Navigator>
      <Stack.Screen name="Home" component={HomeScreen} />
      <Stack.Screen name="Property" component={PropertyScreen} />
    </Stack.Navigator>
  </NavigationContainer>
);
```

---

## 3. **React Native Hooks and Forms**

### 3.1 Definition
Hooks manage state and lifecycle; Formik/React Hook Form handle form inputs [cite: 152].

### 3.2 Example: Form with React Hook Form
```jsx
import { useForm } from 'react-hook-form';
const PropertyForm = () => {
  const { register, handleSubmit } = useForm();
  const onSubmit = data => console.log(data);
  return (
    <View>
      <TextInput {...register('name')} placeholder="Property Name" />
      <Button title="Submit" onPress={handleSubmit(onSubmit)} />
    </View>
  );
};
```

---

## 4. **State Management**

### 4.1 Definition
Redux or MobX manages app-wide state for consistency [cite: 156].

### 4.2 Example: Redux Store
```jsx
import { configureStore } from '@reduxjs/toolkit';
const store = configureStore({
  reducer: { properties: propertiesReducer },
});
```

---

## 5. **Performing Tests**

### 5.1 Definition
Unit tests verify component functionality using Jest [cite: 160].

### 5.2 Example: Jest Test
```jsx
import { render } from '@testing-library/react-native';
test('renders property', () => {
  const { getByText } = render(<Property name="Villa" price="500000" />);
  expect(getByText('Villa - $500000')).toBeTruthy();
});
```

---

## ✅ Summary Table
| Concept               | Description                              | Example                        |
|-----------------------|------------------------------------------|--------------------------------|
| React Native          | Building UI with components              | Property component             |
| Navigation            | Screen transitions                       | React Navigation stack         |
| Hooks/Forms           | Managing state and inputs                | React Hook Form for property   |
| State Management      | App-wide data consistency                | Redux store setup              |
| Testing               | Verifying functionality                   | Jest unit test                 |

---

## 📚 Practice Exercises
1. Create a React Native component for displaying property details [cite: 148].
2. Implement navigation between home and property details screens [cite: 150].
3. Write a Jest test for a form submission component [cite: 160].