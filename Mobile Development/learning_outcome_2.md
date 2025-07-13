# Learning Outcome 2: Design the Mobile App

This section addresses the key design elements required for developing effective cross-platform mobile applications using React Native. It aligns with the SPECM502 module’s emphasis on user-centric design practices and prepares learners to deliver high-quality mobile app interfaces, particularly in the context of the RealEstatePro project.

---

## 1. Mobile App Assets

### Icons

**Purpose:**
Icons serve as visual representations of actions, features, or content, enhancing usability and navigation.

**Design Considerations:**

* Use vector formats (e.g., SVG) for resolution independence.
* Follow platform-specific design standards:

  * Material Design (Android)
  * Human Interface Guidelines (iOS)
* Ensure icons are intuitive and context-appropriate (e.g., a house icon for property listings).

**Implementation in React Native:**

* Use the `react-native-vector-icons` package with sets like FontAwesome or Material Icons.
* Customize appearance through `size`, `color`, and `style` props.

---

### Splash Screen

**Purpose:**
The splash screen provides a visual introduction while the app loads, contributing to branding and perceived performance.

**Design Considerations:**

* Incorporate the app logo, name, and a clean background.
* Minimize complexity for fast rendering and compatibility across devices.
* Account for multiple screen resolutions and aspect ratios.

**Implementation in React Native:**

* Configure splash assets in:

  * Android: `android/app/src/main/res/drawable`
  * iOS: `Images.xcassets` in Xcode
* Use `react-native-splash-screen` to control visibility programmatically.

---

### Colors

**Purpose:**
A color palette influences the app’s mood, readability, and brand identity.

**Design Considerations:**

* Define primary, secondary, and accent colors (e.g., RealEstatePro might use blue-grays for a professional look).
* Ensure WCAG 2.1 compliance for text contrast (minimum 4.5:1).
* Support both light and dark modes.

**Implementation in React Native:**

* Centralize in a theme file (e.g., `theme.js`) using JavaScript objects.
* Example:

  ```js
  const theme = { primary: '#1E88E5', secondary: '#757575' };
  ```

---

### Themes

**Purpose:**
Themes ensure visual consistency and enable dynamic user preferences (e.g., light/dark modes).

**Design Considerations:**

* Maintain uniformity in component styling (buttons, text, icons).
* Optionally support role-based theming (e.g., different themes for admins vs. clients).

**Implementation in React Native:**

* Use React Context API or third-party libraries like `react-native-paper` for theme management.

---

### Fonts

**Purpose:**
Typography affects readability, brand alignment, and accessibility.

**Design Considerations:**

* Choose platform-aligned fonts (e.g., Roboto for Android, San Francisco for iOS).
* Limit font variants to improve performance and design clarity.
* Ensure text scalability for accessibility.

**Implementation in React Native:**

* Add fonts under `assets/fonts/` and register them in `react-native.config.js`.
* Apply fonts using `fontFamily` style properties.

---

## 2. Wireframes and Mockups

### Sketching and Ideation

**Purpose:**
Sketching translates ideas into visual structures, facilitating early feedback and iteration.

**Process:**

* Define user roles and key actions (admin CRUD, client browsing, agent updates).
* Start with low-fidelity sketches outlining layout and navigation.
* Iterate based on feedback before transitioning to high-fidelity mockups.

**Tools and Techniques:**

* Quick sketches: Paper, Balsamiq.
* Wireframe tools: Figma, Adobe XD.

---

### Figma and Adobe XD

**Figma:**

* Cloud-based tool supporting collaboration, reusable components, and plugin integration.
* Suitable for RealEstatePro dashboards, forms, and listing views.

**Adobe XD:**

* Ideal for high-fidelity, artboard-based design.
* Supports interactive transitions and Adobe ecosystem integration.

**Workflow:**

1. Create wireframes to define layout and flow.
2. Build mockups with finalized colors, typography, and UI elements.
3. Export assets (e.g., icons, illustrations) for development.

---

### UI Design Principles

**Responsive Design:**

* Use flexible units and layout tools like Flexbox to adapt across devices.
* React Native tools: `Dimensions` API, `react-native-responsive-screen`.

**Layouts:**

* Grid-based layout (e.g., 8pt spacing system) for visual consistency.
* Use Flexbox properties: `flexDirection`, `justifyContent`, `alignItems`.

**UI Elements:**

* Create modular, reusable components (e.g., cards, buttons).
* Ensure touch targets are accessible (≥48x48 pixels).
* Support screen readers with accessible labels and roles.

**RealEstatePro Examples:**

* A card component displaying property image, name, price, and buttons.
* Separate UI flows for:

  * Admin (management tools)
  * Client (browsing interface)
  * Agent (update interface)

---

## 3. Prototypes

### Defining User Flows

**Purpose:**
User flows define how different users interact with the app, ensuring intuitive navigation and task fulfillment.

**Process:**

* Identify main goals per role.
* Map screens and interactions in flowcharts.
* Validate flows with users or stakeholders.

**RealEstatePro Examples:**

* **Client:** Sign up → Browse listings → View details → Add to wishlist → Submit request.
* **Admin:** Login → Dashboard → Manage properties → Manage agents.
* **Agent:** Login → View/edit listings → Update property details.

---

### Navigation Design

**Common Navigation Patterns:**

* **Stack Navigation**: Linear flows (e.g., Login → Home → Details).
* **Tab Navigation**: Quick access to core sections (e.g., Home, Favorites, Profile).
* **Drawer Navigation**: Secondary navigation options (e.g., Settings, Logout).

**Design Considerations:**

* Align with platform standards (e.g., swipe gestures on Android, back button on iOS).
* Limit interaction steps (ideally ≤3 taps for primary actions).

**Implementation in React Native:**

* Use `react-navigation` library and configure navigators:

  ```js
  createStackNavigator(), createBottomTabNavigator(), createDrawerNavigator()
  ```

---

### Interactive Elements

**Buttons:**

* Provide feedback on interaction (e.g., visual state change).
* Use `TouchableOpacity` or `Pressable` components for responsiveness.

**Animations:**

* Enhance experience with transitions (e.g., modals, cards).
* Libraries: `react-native-reanimated`, React Native’s `Animated` API.

**Interactive Components:**

* Forms: Use `formik` or `react-hook-form` for robust validation and form control.
* Carousels: Display image galleries using `react-native-snap-carousel`.

---

## Summary and Key Takeaways

| Topic                | Key Points                                                                    |
| -------------------- | ----------------------------------------------------------------------------- |
| Mobile App Assets    | Define icons, colors, fonts, splash screens, and themes for brand consistency |
| Wireframes & Mockups | Use Figma or Adobe XD to translate ideas into structured, high-fidelity UI    |
| Prototypes           | Build user flows, interactive elements, and navigations for intuitive UX      |
