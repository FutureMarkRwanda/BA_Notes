# Learning Outcome 3: Develop Front End with React Native

This section outlines the foundational skills and tools required to develop the front end of a cross-platform mobile application using React Native. It covers JSX syntax, component architecture, navigation patterns, React hooks, forms, state management, and testing. These are applied in the context of the **RealEstatePro** project and aligned with the objectives of the SPECM502 module.

---

## 1. React Native Fundamentals

### JSX Syntax

**Purpose:** JSX (JavaScript XML) is a syntax extension used in React Native for writing UI components declaratively.

**Key Concepts:**

* Combines HTML-like syntax with JavaScript logic.
* Supports embedding dynamic expressions, conditionals, and loops.
* Each component must return a single root element (e.g., wrapped in `<View>`).

**Example (RealEstatePro):**

```jsx
<View>
  <Text>{property.name}</Text>
  <Image source={{ uri: property.image }} />
</View>
```

---

### Components

**Purpose:** Components are the building blocks of React Native apps and promote reusability and modularity.

**Types:**

* **Functional Components** (preferred): Use hooks (`useState`, `useEffect`) for state and lifecycle handling.
* **Class Components** (legacy): Use lifecycle methods like `componentDidMount`.

**Core Components:**

* `<View>`, `<Text>`, `<Image>`, `<TouchableOpacity>`, `<ScrollView>`

**Example:**
Create a reusable `PropertyCard` component for displaying a property's image, name, and price.

---

### Props and State

**Props:**

* Immutable data passed from parent to child.
* Enable component customization.

```jsx
<PropertyCard name="Villa" price={500000} />
```

**State:**

* Local, mutable data using `useState` or `this.setState`.
* Changes to state trigger UI re-renders.

**Example (RealEstatePro):**

```jsx
const [name, setName] = useState('');
```

---

## 2. UI Navigation

### Navigation Patterns (React Navigation Library)

* **Stack Navigation (`createStackNavigator`)**

  * Linear flows (e.g., Login → Dashboard → Details).
  * Supports screen transitions and header customization.

* **Tab Navigation (`createBottomTabNavigator`)**

  * Provides access to primary screens via bottom or top tabs.
  * Customizable with icons and labels.

* **Drawer Navigation (`createDrawerNavigator`)**

  * Sidebar menu for secondary options (e.g., Settings, Logout).

**RealEstatePro Use Cases:**

* Stack: Login → Property List → Details
* Tabs: Client dashboard navigation (Home, Search, Wishlist)
* Drawer: Admin settings (Manage Agents, Reports)

---

## 3. Hooks

### Built-in Hooks

* **`useState`**: Manage component-local state.
* **`useEffect`**: Handle side effects like API calls.
* **`useContext`**: Access global context (e.g., authentication state).
* **`useRef`**: Access DOM elements or persist values across renders.
* **`useCallback`**: Memoize functions to prevent unnecessary re-renders.
* **`useMemo`**: Memoize computed values for performance.

**Examples:**

```jsx
const [loading, setLoading] = useState(false);

useEffect(() => {
  fetchProperties();
}, []);

const filtered = useMemo(() => properties.filter(p => p.price > 100000), [properties]);
```


### Custom Hooks and Testing

**Custom Hooks:**

* Encapsulate reusable logic (e.g., `usePropertyForm`, `useFetchProperties`).

**Testing Hooks:**

* Use `@testing-library/react-hooks` to isolate and test hook logic.

**RealEstatePro Example:**

* Custom hook `usePropertyForm` to manage form state and validation logic for property submission.

---

## 4. Forms

### Form Design and Validation

* Use `<TextInput>` for form fields and `<TouchableOpacity>` for submission.
* Ensure mobile accessibility and keyboard interaction.

**Libraries:**

* **Formik**: Full-featured form management and validation.
* **React Hook Form**: Lightweight alternative optimized for performance.

**Example (Formik):**

```jsx
<Formik
  initialValues={{ name: '' }}
  validate={values => (!values.name ? { name: 'Required' } : {})}
  onSubmit={handleSubmit}
/>
```

**RealEstatePro Example:**

* Design a form for agents to submit new properties with fields such as name, address, price, room count, and images.

---

### Event Handling and Submission

**Event Handling:**

* Handle changes via `onChangeText`, focus, blur, and button `onPress`.

**Submission:**

* Validate inputs.
* Use async functions to send data to backend APIs.
* Display loading states and handle errors gracefully.

**Example:**

```jsx
const onSubmit = async (data) => {
  try {
    setLoading(true);
    await axios.post('/api/properties', data);
  } catch (error) {
    console.error(error);
  } finally {
    setLoading(false);
  }
};
```

---

## 5. State Management

### Local vs Global State

* **Local State:** For UI-specific data (e.g., modals, form inputs).

  * `useState`, `useReducer`

* **Global State:** For shared application state.

  * **Redux:** Centralized store with reducers and actions.
  * **Context API:** Lightweight alternative for simple apps.
  * **MobX:** Observable state and auto-tracked reactions.

**RealEstatePro Example:**

* Use Redux to store authenticated user info and property listings.
* Use local state for form input within components.

---

### Normalization and Denormalization

* **Normalization:**

  * Store flat, scalable data structures.
  * Example:

    ```js
    {
      properties: {
        byId: {
          1: { id: 1, name: "Villa", ownerId: 2 },
          2: { id: 2, name: "Apartment", ownerId: 3 }
        }
      }
    }
    ```

* **Denormalization:**

  * Combine related data for UI rendering.
  * Easier to access for presentation but less efficient for updates.

**RealEstatePro Example:**

* Normalize data in Redux and denormalize in components for display (e.g., show owner info within property cards).

---

## 6. Testing

### Types of Testing

| Type                    | Purpose                                          | Tools                 |
| ----------------------- | ------------------------------------------------ | --------------------- |
| **Unit Testing**        | Test functions/components in isolation           | Jest                  |
| **Component Testing**   | Test visual components and interactions          | React Testing Library |
| **Integration Testing** | Test interactions between components or features | React Testing Library |
| **End-to-End Testing**  | Test full app workflows on devices/emulators     | Detox                 |
| **Async Testing**       | Test data fetching and asynchronous logic        | Jest, waitFor, act    |

---

### Tools

* **Jest**: Unit and integration tests, mocking and assertions.
* **React Testing Library**: UI testing via simulated user interactions.
* **Detox**: E2E testing for mobile workflows.

**RealEstatePro Examples:**

* Unit test a price formatter utility function.
* Component test `PropertyCard` rendering.
* Use Detox to test adding a property to a client’s wishlist from login through to submission.

---

## Summary of Key Concepts

| Area             | Key Focus                                                                 |
| ---------------- | ------------------------------------------------------------------------- |
| JSX & Components | Enables modular, reusable UI structure using declarative syntax           |
| Navigation       | React Navigation supports complex flows across user roles                 |
| Hooks            | Simplify state, effects, and context handling across components           |
| Forms            | Managed efficiently with Formik or React Hook Form, with validation logic |
| State Management | Combination of local/global state with normalization ensures scalability  |
| Testing          | Verifies correctness and reliability through layered test strategies      |
