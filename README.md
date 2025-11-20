# 📍 PlacePicker: A React Project for Learning Hooks

> **A React application demonstrating state management, side effects, and asynchronous operations using `useState`, `useEffect`, and `useCallback` to save and display selected places.**

---

## 🧠 Key Learning Points

This project was an excellent way to solidify understanding of the following concepts:

### 1. React Hooks

| Concept | Usage in Project | Why it was used |
| :--- | :--- | :--- |
| **`useState`** | Managing component-specific state, such as `pickedPlaces`, `modalIsOpen`, and `remainingTime`. | To make components interactive and manage data that changes over time. |
| **`useEffect`** | 1. Fetching the user's current geolocation. 2. Setting up the auto-confirm **`setTimeout`** in `DeleteConfirmation`. 3. Setting up the progress bar **`setInterval`**. 4. Opening/closing the `<dialog>` element in the `Modal` component. | To execute side effects (API calls, timers) after rendering, and to clean them up (e.g., `clearTimeout`, `clearInterval`). |
| **`useRef`** | Storing the ID of the place to be removed (`selectedPlace`) and getting a direct reference to the `<dialog>` DOM element. | For values that should **not** trigger a re-render when they change, or to directly interact with DOM elements (like calling `showModal()`). |
| **`useCallback`** | Wrapping the `handleRemovePlace` function. | To **memoize** the function, preventing it from being re-created on every render. This is crucial here because `handleRemovePlace` is a dependency in the `DeleteConfirmation`'s `useEffect` (for `setTimeout`), which prevents the timer from resetting unnecessarily. |

---

### 2. Browser APIs & Utilities

* **`setTimeout` & `clearTimeout`**: Used in `DeleteConfirmation` to automatically confirm the deletion after 3 seconds, demonstrating how to use and **clean up** timers with `useEffect`.
* **`setInterval` & `clearInterval`**: Used in `DeleteConfirmation` (and the separate `ProgressBar` component, if you kept it) to drive the visual progress bar animation, showing continuous updates and cleanup.
* **`localStorage`**: Used to persist the `selectedPlaces` IDs across browser sessions, ensuring the picked places are saved when the user closes and reopens the app.
* **HTML `<dialog>` Element**: Utilized in the `Modal` component, along with `useRef` and `useEffect`, to manage a native, accessible modal window via the `showModal()` and `close()` methods.
* **`createPortal`**: Used in the `Modal` component to render the modal's content outside of the component's normal DOM hierarchy, typically at a root element like `document.getElementById('modal')`, to prevent styling issues.

---

## 🛠️ Project Structure Highlights

The application is structured around several components that manage specific parts of the UI and logic:

* **`App.jsx`**: Manages the main state (`pickedPlaces`, `availablePlaces`), handles user interaction functions (`handleSelectPlace`, `handleRemovePlace`), and coordinates the application flow.
* **`DeleteConfirmation.jsx`**: Houses the logic for the auto-confirm timer (`setTimeout`) and the progress bar interval (`setInterval`).
* **`Modal.jsx`**: A reusable wrapper that uses **`createPortal`** and the **`useRef`/`useEffect`** pattern to control the native HTML `<dialog>` element.
