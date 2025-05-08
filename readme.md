## Differences Between Interfaces and Types in TypeScript
In TypeScript, both interfaces and types allow you to define custom types for objects, but there are some important differences between them. Here is the differences,

1. Syntax:
Interfaces are declared using the interface keyword:
 interface Person {
  name: string;
  age: number;
}

Types are declared using the type keyword:
type Person = {
  name: string;
  age: number;
}

While both are similar in how they allow you to define an object’s structure, the syntax is different.

2. Extending or Merging:
Interfaces can be extended using the extends keyword or even merged if you declare them with the same name:
interface Person {
  name: string;
  age: number;
}

interface Person {
  email: string;  // merging with the 1st interface
}

const person: Person = {
  name: "Alice",
  age: 25,
  email: "alice@example.com"
};
Types cannot be merged. Once you define a type, it is fixed. However, you can extend it using intersection types:
type Person = {
  name: string;
  age: number;
};
type Contact = Person & { email: string };
const contact: Contact = {
  name: "Alice",
  age: 25,
  email: "alice@example.com"
};

3. Use Cases:
Interfaces are mainly used when you want to define the structure of an object or class. They are better for OOP and class-based models.

Types are more versatile and can be used not only for object shapes but also for primitives, unions, intersections, and tuples. They offer more flexibility compared to interfaces.

4. Union Types:
Types can represent union types, meaning they can accept multiple different types:
type ID = string | number;

Interfaces cannot directly represent union types. If you want to create union types with interfaces, you would need to use a workaround, such as using a type with interface in an intersection.

5. Compatibility:
Interfaces and types are generally compatible with each other. In most cases, an interface and a type can be used interchangeably for object-like structures. However, interfaces are more suited for extension and declaration merging.

Types offer greater flexibility, allowing for the combination of different types into one, such as unions or intersections.

6. Performance:
There is no significant performance difference between interfaces and types during runtime. But using declaration merging, interfaces can be more efficient in certain cases because TypeScript handles them as separate declarations.

In Summary:
Use interfaces when working with object-oriented designs or when you want to take advantage of features like declaration merging and extension.

Use types when you need more flexibility, such as defining union types, intersection types, or tuple types.


## What is the use of the keyof keyword in TypeScript?
The keyof keyword in TypeScript is used to get the keys (property names) of an object as a type. It returns a union type made up of the object’s keys. This is useful when you want to create type-safe, reusable, and generic functions or types that work with object properties.

Why is it useful?
It prevents you from using wrong property names by mistake.
It improves code safety and auto-completion in editors.
It’s helpful when building functions that should work with dynamic keys.

Example:
type Person = {
  name: string;
  age: number;
};
type PersonKeys = keyof Person;
// PersonKeys = "name" | "age"
Now you can use PersonKeys as a type that allows only "name" or "age" — nothing else.

Using keyof in a function
function getValue<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { name: "Alice", age: 25 };
const value = getValue(user, "name"); // returns "Alice"

This function only allows valid keys from the object, thanks to keyof.