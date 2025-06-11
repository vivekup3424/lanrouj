In TypeScript, both `unknown` and `any` are used to represent values with unknown types, but they have key differences in terms of type safety.

### 1. `any`

- **Completely disables type checking**: Assigning a value of type `any` allows any operation without type checking.
- **Unsafe**: You can perform any operation on an `any`-typed value without TypeScript complaining.
- **Use case**: When you need to temporarily escape type checking (e.g., migrating JavaScript code to TypeScript).

#### Example:

```ts
let value: any;
value = 42;
value = "hello";
value.toUpperCase(); // No error, even if value is not guaranteed to be a string
```

---

### 2. `unknown`

- **Type-safe counterpart of `any`**: You cannot perform operations on `unknown` without first checking its type.
- **Forces type checks**: You need to use type assertions or checks before using the value.
- **Use case**: When dealing with values of unknown types while maintaining type safety.

#### Example:

```ts
let value: unknown;
value = 42;
value = "hello";
// value.toUpperCase(); ❌ Error: Object is of type 'unknown'

// Safe way to use unknown:
if (typeof value === "string") {
  console.log(value.toUpperCase()); // ✅ Now it's safe
}
```

---

### Summary:

|Feature|`any`|`unknown`|
|---|---|---|
|Type safety|❌ No safety|✅ Type-safe|
|Type checking|❌ No type checks|✅ Requires checks before use|
|Use case|Escape TypeScript checks|Handle unknown data safely|

So, use `unknown` when you want type safety and `any` only when you absolutely need to bypass type checks.