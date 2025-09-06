# javascript-reactjs-common-errors

# JS-ReactJS-Common-Errors

## 1. Optional Chaining (`?.`) Error in JavaScript

### **Problem:**
Using `setResults(data.recipes || [])` may throw an error if `data` is `undefined` or `null`.

### **Error Explanation:**
If `data` is `undefined` or `null`, then accessing `data.recipes` directly will cause a runtime error:
```js
setResults(data.recipes || []); // ❌ TypeError: Cannot read properties of undefined (reading 'recipes')
```

### **Solution:**
Use **optional chaining (`?.`)** to safely access `data.recipes`:
```js
setResults(data?.recipes || []); // ✅ No error, safely assigns []
```
This ensures that if `data` is `undefined` or `null`, `setResults([])` is executed instead of throwing an error.

**Corrected:**  
"I'll give you the format: ..." (Your sentence is already fine since you're giving a context.)

---

Here’s your new entry following your format `# javascript-reactjs-common-errors`:

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

  input.value = words; // input.value will be an array (e.g., ["Hello", "World"])
}
```
This causes `input.value` to be set as a string representation of an array (like `"Hello,World"`), or behaves unpredictably in some cases.

---

### **Solution:**
Use `.join(" ")` to convert the array back into a string before assigning it:
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
This ensures that `input.value` is a clean, properly formatted string.

---



---

## 3. QuotaExceededError caused by storing large image data in localStorage.

### 🧨 Error:
```

Uncaught QuotaExceededError: Failed to execute 'setItem' on 'Storage': Setting the value of 'cart' exceeded the quota.

````

### ✅ Fix:
- Avoid storing large binary data (like images) in `localStorage`
- Serve images on-demand via backend

### 💡 Code Example:
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
````

---

## 📚 Topics Covered


## 4. Warning: Invalid DOM property `class`. Did you mean `className`?
```js
// ❌ Error: Using wrong attribute in JSX
<div class="container">Hello World</div>
```

👉 This gives the error:

```
Warning: Invalid DOM property `class`. Did you mean `className`?
```

✅ Fix:

```js
<div className="container">Hello World</div>
```

