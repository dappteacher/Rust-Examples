#### ⚡ What is Inline Code?

In Rust, **inline code** usually refers to:

1. Writing simple expressions or logic directly inside a function.
2. Using the `#[inline]` attribute to suggest inlining a function for performance reasons.
3. Using **inline blocks** (code blocks inside other blocks) to manage **scoping** and **temporary variables**.

---

## 🧱 Inline Blocks and Scope: Explained

Rust allows you to define **code blocks `{}` inside other blocks**, and each block has its own **scope**. Variables defined inside a block are **not accessible outside** that block.

---

### 🔍 Example Explained

```rust
fn main() {
    let number1 = 25;

    {
        let number2 = 16;
        println!("{}", number2);  // OK: prints 16
    }

    println!("{}", number2);     // ❌ ERROR: `number2` is not defined
}
```

#### ✅ What's happening here:

1. `let number1 = 25;`
   This declares a variable in the **outer scope**.

2. `{ let number2 = 16; ... }`
   This block creates a **new scope**.
   The variable `number2` only exists **inside** this block.
   `println!("{}", number2);` is fine **inside** this scope.

3. `println!("{}", number2);`
   ❌ This will cause a **compiler error**: `cannot find value number2 in this scope`.
   You likely meant to use `number1`, which was declared earlier.

---

### ✅ Corrected Version:

```rust
fn main() {
    let number1 = 25;

    {
        let number = 16;
        println!("Inner number: {}", number); // prints 16
    }

    println!("Outer number: {}", number1); // prints 25
}
```

---

## 📦 Key Concepts:

| Concept             | Description                                                                  |
| ------------------- | ---------------------------------------------------------------------------- |
| **Inline block**    | A `{}` block inside a function or another block.                             |
| **Scope**           | Each block defines a new scope; variables are only valid inside their scope. |
| **Shadowing**       | You can redeclare a variable with the same name in a new scope.              |
| **Compiler safety** | Rust ensures variables aren’t used outside their declared scopes.            |

---

## 🧠 Takeaway

Inline code blocks are useful for:

* Temporary logic or helper variables.
* Limiting variable visibility and lifetime.
* Structuring code for readability and correctness.

---

#### ⚡ Other Inline Codes

---

## 🧱 1. Writing Code Inline in Functions

Rust encourages clear and readable inline expressions inside functions. Here's a simple example:

```rust
fn main() {
    let a = 5;
    let b = 10;

    let sum = a + b; // Inline operation

    println!("Sum is: {}", sum);
}
```

Inline operations like `a + b` are very common and make your code concise and readable.

---

## 🚀 2. The `#[inline]` Attribute

The `#[inline]` attribute **suggests** to the compiler that a function should be inlined. Inlining means **copying the function's code directly** where it's called, to avoid function call overhead.

### ✅ Basic Usage:

```rust
#[inline]
fn add(x: i32, y: i32) -> i32 {
    x + y
}

fn main() {
    let result = add(3, 4);
    println!("Result: {}", result);
}
```

---

## 📦 When to Use `#[inline]`?

* For **small and frequently used functions**.
* In **performance-critical code**, especially in libraries.
* Not needed for most application code; Rust already inlines aggressively when it sees fit.

---

## ⚠️ Notes:

* Inlining is only a *suggestion*, not a command. The compiler decides based on optimization settings.
* You can use `#[inline(always)]` to force inlining (not always recommended).
* Overuse of inlining may increase binary size.

---

## 🧪 Example: `#[inline(always)]`

```rust
#[inline(always)]
fn multiply(a: i32, b: i32) -> i32 {
    a * b
}

fn main() {
    println!("6 * 7 = {}", multiply(6, 7));
}
```

Use this only if you **know** it improves performance and doesn't cause code bloat.

---

## ✅ Summary

| Concept             | Use Case                                     |
| ------------------- | -------------------------------------------- |
| Inline expressions  | Write simple logic directly inside functions |
| `#[inline]`         | Suggest compiler to inline for performance   |
| `#[inline(always)]` | Force inlining (use with caution)            |

---

