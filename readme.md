## Differences Between Interfaces and Types in TypeScript

In TypeScript, both `interface` and `type` can be used to define the structure of data. However, there are important differences that influence when you should use one over the other.

### # Syntax

**Interface:**

```ts
interface Person {
  name: string;
  age: number;
}
```

**Type:**

```ts
type Person = {
  name: string;
  age: number;
};
```

Though they define the structure similarly, the syntax is different.

### # Extending or Merging

**Interface:** Supports `extends` and declaration merging.

```ts
interface Person {
  name: string;
  age: number;
}

interface Person {
  email: string;
}

const person: Person = {
  name: "sumaya",
  age: 24,
  email: "sumaya@gmail.com"
};
```

**Type:** Cannot be merged, but can be extended using intersections.

```ts
type Person = {
  name: string;
  age: number;
};

type Contact = Person & { email: string };

const contact: Contact = {
  name: "sumaya",
  age: 24,
  email: "sumaya@example.com"
};
```

### # Use Cases

* **Interfaces** are preferred in object-oriented design and when defining the shape of classes or objects.
* **Types** are more versatile and can define unions, intersections, tuples, and primitive types.

### # Union Types

**Type:**

```ts
type ID = string | number;
```

**Interface:** Cannot directly define union types.

### # Compatibility

* Interfaces and types can often be used interchangeably.
* Interfaces are better for extension and merging.
* Types are more flexible for complex combinations.

### # Performance

There's no runtime performance difference. But interfaces may have slight compile-time benefits due to merging.

### # Summary

* Use **interface** for OOP style, classes, and merging.
* Use **type** when you need unions, intersections, or more flexibility.

---

## What is the use of the `keyof` keyword in TypeScript?

The `keyof` keyword is used to extract the keys of an object type as a union of string literal types. It helps ensure you’re using valid property names and makes your code more type-safe and generic.

### # Why use `keyof`?

* Prevents mistakes by enforcing valid keys.
* Improves auto-completion.
* Great for building reusable and flexible functions.

### # Example

```ts
type Person = {
  name: string;
  age: number;
};

type PersonKeys = keyof Person;  // "name" | "age"
```

Now `PersonKeys` is a type that allows only `"name"` or `"age"`.

### # Using `keyof` in a function

```ts
function getValue<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { name: "sumu", age: 24 };
const value = getValue(user, "name"); // returns "Alice"
```

Thanks to `keyof`, only valid keys from the object can be passed to the function, making it safer and more reliable.
