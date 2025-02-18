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


