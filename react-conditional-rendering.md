# 🔥 React Conditional Rendering: The Complete Guide

In React, **conditional rendering** means showing or hiding components based on a certain condition. This is essential for creating **dynamic UIs** where different content is displayed based on user interaction, authentication status, API responses, etc.

---

## 🚀 Methods of Conditional Rendering in React

### ✅ 1. Using `&&` (Logical AND) – Best for Simple Cases
🔹 **Renders a component only if the condition is `true`.**  
🔹 **If `false`, React ignores it (renders nothing).**

```tsx
const isLoggedIn = true;

return (
  <div>
    <h1>Welcome!</h1>
    {isLoggedIn && <p>You are logged in.</p>}  {/* ✅ Will render */}
    {!isLoggedIn && <p>Please log in.</p>}      {/* ❌ Won't render */}
  </div>
);
```
📌 **If `isLoggedIn === false`, `<p>You are logged in.</p>` won’t appear at all.**

---

### ✅ 2. Using Ternary Operator (`? :`) – Best for `if-else` Cases
🔹 **Use this when you need an "else" case.**  
🔹 **More readable than `if-else` in JSX.**

```tsx
const isLoggedIn = false;

return (
  <div>
    {isLoggedIn ? <p>Welcome back!</p> : <p>Please log in.</p>}
  </div>
);
```
📌 **If `isLoggedIn === true`, it shows `"Welcome back!"`, otherwise `"Please log in."` appears.**

---

### ✅ 3. Using `if` Statement (Outside JSX)
🔹 **Best for complex conditions where JSX gets too messy.**  
🔹 **Cannot be used directly inside JSX.**

```tsx
const isLoggedIn = true;
let content;

if (isLoggedIn) {
  content = <p>Welcome back!</p>;
} else {
  content = <p>Please log in.</p>;
}

return <div>{content}</div>;
```
📌 **This method is useful when you have multiple conditions before rendering.**

---

### ✅ 4. Using Functions for Cleaner Code
🔹 **Extract logic into a function to improve readability.**

```tsx
const renderMessage = (isLoggedIn) => {
  if (isLoggedIn) {
    return <p>Welcome back!</p>;
  } else {
    return <p>Please log in.</p>;
  }
};

return <div>{renderMessage(true)}</div>;
```
📌 **Encapsulating logic in functions helps keep JSX clean.**

---

### ✅ 5. Using `switch` for Multiple Conditions
🔹 **Great for handling many possible cases.**  
🔹 **More readable than multiple `if-else` statements.**

```tsx
const getStatusMessage = (status) => {
  switch (status) {
    case "loading":
      return <p>Loading...</p>;
    case "success":
      return <p>Data Loaded Successfully!</p>;
    case "error":
      return <p>Something went wrong!</p>;
    default:
      return <p>Unknown status</p>;
  }
};

return <div>{getStatusMessage("success")}</div>;
```
📌 **Useful when rendering different UI states based on API responses.**

---

### ✅ 6. Using `return null` to Hide Components
🔹 **Instead of using `&&` or `if-else`, you can return `null` to hide a component.**

```tsx
const WarningMessage = ({ showWarning }) => {
  if (!showWarning) {
    return null; // ❌ Won't render anything
  }
  return <p>Warning: This is important!</p>;
};

return <WarningMessage showWarning={false} />;
```
📌 **React will not render anything if `null` is returned.**

---

### ✅ 7. Using Higher-Order Components (HOC)
🔹 **Wrap components with logic that decides if they should be displayed.**

```tsx
const withAuth = (Component) => (props) => {
  return props.isAuthenticated ? <Component {...props} /> : <p>Access Denied</p>;
};

const Dashboard = () => <h1>Dashboard</h1>;

const ProtectedDashboard = withAuth(Dashboard);

return <ProtectedDashboard isAuthenticated={false} />;
```
📌 **If `isAuthenticated === false`, "Access Denied" will be shown instead of the `Dashboard`.**

---

### ✅ 8. Using `Optional Chaining (?.)` (For API Data)
🔹 **Prevents errors when accessing undefined properties.**

```tsx
const user = null;

return (
  <div>
    <p>Name: {user?.name || "Guest"}</p> {/* Avoids errors if `user` is `null` */}
  </div>
);
```
📌 **If `user === null`, it displays `"Guest"` instead of throwing an error.**

---

## 🏆 Best Practices for Conditional Rendering
✅ **Use `&&` for simple cases.**  
✅ **Use `? :` for `if-else` scenarios.**  
✅ **Use `if` statements outside JSX for better readability.**  
✅ **Extract logic into functions when conditions are complex.**  
✅ **Return `null` to hide components instead of unnecessary conditional checks.**  
✅ **Use `?.` (optional chaining) to prevent errors when accessing API data.**  

---

### 🎯 Final Example: Combining Multiple Conditional Techniques
```tsx
const App = ({ isAuthenticated, userStatus }) => {
  return (
    <div>
      <h1>Welcome to My App</h1>
      {isAuthenticated ? <p>You are logged in.</p> : <p>Please log in.</p>}
      {userStatus === "loading" && <p>Loading user data...</p>}
      {userStatus === "error" && <p>Error loading user data!</p>}
      {userStatus === "success" && <p>Welcome, {user?.name || "Guest"}!</p>}
    </div>
  );
};
```

---

### 🎯 Which Method Should You Use?
| Scenario | Best Method |
|----------|------------|
| Simple condition | `&&` (`{isLoggedIn && <Component />}`) |
| Need an "else" case | Ternary (`{isLoggedIn ? <A /> : <B />}`) |
| Complex conditions | `if` statement outside JSX |
| Multiple conditions | `switch` statement |
| API Data Handling | Optional chaining (`user?.name \|\| "Guest"`) |
| Hide a component | Return `null` |

---

## 🎯 Conclusion
Conditional rendering is a **powerful feature** in React that allows you to dynamically show or hide components. Choosing the right technique **depends on the complexity of the condition** and **the readability of your code**.
