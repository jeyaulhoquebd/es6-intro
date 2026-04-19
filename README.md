# `difference between var let const`

In JavaScript, understanding the nuances between `var`, `let`, and `const` is fundamental to writing clean, predictable code. While they all serve the purpose of declaring variables, they behave differently regarding **scope**, **hoisting**, and **reassignment**.

---

## 1. `var` (The Legacy Way)
Before ES6 (2015), `var` was the only way to declare variables. It has several quirks that can lead to bugs in modern applications.

* **Scope:** Function-scoped. If declared inside a function, it’s available throughout that function. If declared outside, it becomes global. It **ignores** block scope (like `if` statements or `for` loops).
* **Reassignment:** Can be updated and re-declared within the same scope without error.
* **Hoisting:** Variables are hoisted to the top of their scope and initialized as `undefined`.

```javascript
if (true) {
  var name = "Gemini";
}
console.log(name); // "Gemini" (Works because var ignores block scope)
```

---

## 2. `let` (The Modern Standard)
Introduced in ES6, `let` is now the preferred way to declare variables that you expect to change over time.

* **Scope:** **Block-scoped**. It only exists within the curly braces `{}` where it was defined.
* **Reassignment:** Can be updated but **cannot** be re-declared in the same scope.
* **Hoisting:** Hoisted to the top of the block but stays in a "Temporal Dead Zone" (TDZ). Accessing it before declaration results in a `ReferenceError`.

```javascript
if (true) {
  let age = 25;
}
console.log(age); // ReferenceError: age is not defined
```

---

## 3. `const` (The Immutable Intent)
Also introduced in ES6, `const` is for values that should remain constant.

* **Scope:** Block-scoped (just like `let`).
* **Reassignment:** Cannot be updated or re-declared. You must initialize it at the time of declaration.
* **Nuance with Objects:** While you can’t reassign a `const` variable to a new value, you **can** modify the properties of an object or the elements of an array declared with `const`.

```javascript
const colors = ['red', 'blue'];
colors.push('green'); // This works!
// colors = ['yellow']; // TypeError: Assignment to constant variable.
```

---

## Comparison Summary

| Feature | `var` | `let` | `const` |
| :--- | :--- | :--- | :--- |
| **Scope** | Function Scope | Block Scope | Block Scope |
| **Hoisting** | Yes (initialized as `undefined`) | Yes (TDZ, no initialization) | Yes (TDZ, no initialization) |
| **Can be Reassigned?** | Yes | Yes | No |
| **Can be Re-declared?** | Yes | No | No |

---

### Best Practices for Modern Dev
1.  **Default to `const`:** Use it for everything unless you know the value needs to change. This makes your intent clear and prevents accidental overwrites.
2.  **Use `let` for counters/iterators:** Use it in loops or mathematical logic where values must update.
3.  **Avoid `var`:** In modern JavaScript environments, there is rarely a technical reason to use `var`. It creates less predictable code due to its scoping rules.