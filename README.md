
---

# JavaScript-ReactJS Common Errors

A collection of common JavaScript, ReactJS, and TypeScript errors with explanations and solutions.

---

## 1. Optional Chaining (`?.`) Error in JavaScript

### **Problem:**

Using `setResults(data.recipes || [])` may throw an error if `data` is `undefined` or `null`.

### **Error Explanation:**

```js
setResults(data.recipes || []); // ❌ TypeError: Cannot read properties of undefined (reading 'recipes')
```

### **Solution:**

Use **optional chaining (`?.`)** to safely access `data.recipes`:

```js
setResults(data?.recipes || []); // ✅ No error, safely assigns []
```

---

## 2. Assigning Array to `input.value` Without `.join()` in JavaScript

### **Problem:**

Trying to capitalize the first letter of each word and assigning the result directly to `input.value`.

### **Error Explanation:**

```js
function capitalizeWords() {
  const input = document.getElementById("text-input");
  const words = input.value
    .split(" ")
    .map(word => word.charAt(0).toUpperCase() + word.slice(1).toLowerCase());

  input.value = words; // ❌ input.value becomes an array
}
```

### **Solution:**

```js
function capitalizeWords() {
  const input = document.getElementById("text-input");
  const words = input.value
    .split(" ")
    .map(word => word.charAt(0).toUpperCase() + word.slice(1).toLowerCase())
    .join(" "); // ✅ Join the words into a proper sentence

  input.value = words;
}
```

---

## 3. QuotaExceededError caused by storing large image data in localStorage

### **Error:**

```text
Uncaught QuotaExceededError: Failed to execute 'setItem' on 'Storage': Setting the value of 'cart' exceeded the quota.
```

### **Fix:**

* Avoid storing large binary data in `localStorage`.
* Serve images on-demand via backend.

### **Code Example:**

```js
// ✅ Backend (Express)
exports.getProductPhoto = async (req, res) => {
  const product = await Product.findById(req.params.productId).select("photo");
  if (product && product.photo && product.photo.data) {
    res.set("Content-Type", product.photo.contentType);
    return res.send(product.photo.data);
  }
  res.status(404).json({ error: "Photo not found" });
};

// ✅ Frontend (React)
<img
  src={`http://localhost:8000/api/product/photo/${product._id}`}
  alt={product.name}
/>
```

---

## 4. Warning: Invalid DOM property `class`. Did you mean `className`?

### **Problem:**

```js
<div class="container">Hello World</div> // ❌ Error in JSX
```

### **Error Explanation:**

```
Warning: Invalid DOM property `class`. Did you mean `className`?
```

### **Solution:**

```js
<div className="container">Hello World</div> // ✅ Correct JSX
```

---

## 5. React + TypeScript: `Could not find a declaration file for module '...'`

### **Error Example:**

```text
Could not find a declaration file for module '../components/Profile'. 
'/nodebox/src/components/Profile.js' implicitly has an 'any' type. 
typescript(7016)
```

### **Cause:**

* Importing a **JavaScript file (`.js`)** into a **TypeScript project**.
* TypeScript cannot find type information for the module.

### **Solutions:**

1. **Convert JS to TSX**

```ts
// Profile.tsx
type ProfileProps = { name: string };

const Profile: React.FC<ProfileProps> = ({ name }) => {
  return <div>{name}</div>;
};

export default Profile;
```

2. **Create a declaration file** (keep `.js` file)

```ts
// src/components/Profile.d.ts
declare module "../components/Profile" {
  const Profile: React.ComponentType<any>;
  export default Profile;
}
```

3. **Allow JS imports in tsconfig.json** (less recommended)

```json
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": false
  }
}
```

### **Key Takeaways:**

* TypeScript requires type definitions for all imported modules.
* Converting JS files to TSX is the most robust solution in a React + TypeScript project.

---

## 📚 Topics Covered

* Optional chaining (`?.`) errors
* Array assignment to input fields
* `QuotaExceededError` in localStorage
* JSX `className` warnings
* React + TypeScript import declaration errors

---
