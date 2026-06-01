Rust provides a rich set of data types that can be broadly categorized into scalar types and compound types. 
Here's an overview of the main data types in Rust:

### Scalar Types

1. **Integers**: Both signed and unsigned integers of various sizes.
   - Signed: `i8`, `i16`, `i32`, `i64`, `i128`, `isize`
   - Unsigned: `u8`, `u16`, `u32`, `u64`, `u128`, `usize`

2. **Floating-Point Numbers**: For fractional numbers.
   - `f32` (32-bit floating-point)
   - `f64` (64-bit floating-point)

3. **Boolean**: Represents a true or false value.
   - `bool` (values: `true`, `false`)

4. **Character**: Represents a single Unicode scalar value.
   - `char` (e.g., `'a'`, `'α'`, `'∞'`)

---

In Rust, integer types come in **signed** (`i8`, `i16`, `i32`, `i64`, `i128`, `isize`) and **unsigned** (`u8`, `u16`, `u32`, `u64`, `u128`, `usize`) variants.

## Unsigned Integers (`u*`)

Unsigned integers can only store non-negative values.

| Type   | Range                                                    |
| ------ | -------------------------------------------------------- |
| `u8`   | 0 to 255                                                 |
| `u16`  | 0 to 65,535                                              |
| `u32`  | 0 to 4,294,967,295                                       |
| `u64`  | 0 to 18,446,744,073,709,551,615                          |
| `u128` | 0 to 340,282,366,920,938,463,463,374,607,431,768,211,455 |

Formula:

```text
0 to 2^N - 1
```

where `N` is the number of bits.

---

## Signed Integers (`i*`)

Signed integers can store both positive and negative values using **two's complement** representation.

| Type   | Range                                                                                                       |
| ------ | ----------------------------------------------------------------------------------------------------------- |
| `i8`   | -128 to 127                                                                                                 |
| `i16`  | -32,768 to 32,767                                                                                           |
| `i32`  | -2,147,483,648 to 2,147,483,647                                                                             |
| `i64`  | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807                                                     |
| `i128` | -170,141,183,460,469,231,731,687,303,715,884,105,728 to 170,141,183,460,469,231,731,687,303,715,884,105,727 |

Formula:

```text
-(2^(N-1)) to 2^(N-1) - 1
```

where `N` is the number of bits.

---

## `usize` and `isize`

These depend on the target architecture.

### On a 64-bit system

| Type    | Range                                                   |
| ------- | ------------------------------------------------------- |
| `usize` | 0 to 18,446,744,073,709,551,615                         |
| `isize` | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |

### On a 32-bit system

| Type    | Range                           |
| ------- | ------------------------------- |
| `usize` | 0 to 4,294,967,295              |
| `isize` | -2,147,483,648 to 2,147,483,647 |

`usize` is commonly used for:

* Array indices
* Vector lengths
* Memory sizes

---

## Finding the Limits Programmatically

Rust provides associated constants:

```rust
println!("u64 max = {}", u64::MAX);
println!("u64 min = {}", u64::MIN);

println!("i64 max = {}", i64::MAX);
println!("i64 min = {}", i64::MIN);
```

Output:

```text
u64 max = 18446744073709551615
u64 min = 0

i64 max = 9223372036854775807
i64 min = -9223372036854775808
```

### Interview Tip

A common interview question is:

> Why is `i64::MAX` equal to `2^63 - 1` instead of `2^63`?

Because one bit is reserved for the sign in two's complement representation, leaving only 63 bits for the magnitude. The pattern with all bits set (`111...111`) represents `-1`, not the largest positive number.
