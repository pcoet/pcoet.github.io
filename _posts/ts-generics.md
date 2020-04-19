---
title: Using generics
category: TypeScript
---

To help make code more reusable, TypeScript provides generics. If you're a Java or C# developer you're probably already familiar with generic types. If not, this post should help you understand what they are and how to use them.

JavaScript defines [primitive](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) types (e.g. String, Number, Boolean), the [null](https://developer.mozilla.org/en-US/docs/Glossary/null) type, an [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) type, and a [Function](https://developer.mozilla.org/en-US/docs/Glossary/Function) type derived from Object. TypeScript adds more, including the generic type, which represents a range of types.

You can use the generic type to make functions, classes, or interfaces operate over the set of all types or a subset of types. To define a generic type, you use a type variable in angle brackets: `<T>`. By convention, `T` is often used for the type parameter, but the type variable name can be anything.

## Generic classes

Let's look at an example of a generic class:

```typescript
/**
 * A stack implemented on an array.
 */
class Stack<T> {
  private items: T[];

  constructor() {
    this.items = [];
  }
  push(item: T): void {
    this.items.push(item);
  }
  pop(): T | undefined {
    return this.items.pop();
  }
  peek(): T | undefined {
    return this.items[this.items.length - 1];
  }
  size(): number {
    return this.items.length;
  }
  isEmpty(): boolean {
    if (this.items.length === 0) {
      return true;
    }
    return false;
  }
}
```

The first thing to notice here is the type parameter `T` in the class declaration. The type parameter is a placeholder for a type that will be provided when the class is instantiated. In this case, there are no constraints on the type, so it can be any type.

Why would we want to make this class generic? Well, let's think about a stack data structure. We use a stack as an interface to a collection of items. A stack lets you push an element onto the end of the collection (i.e. the top of the stack) and pop (i.e. remove and return) an element from the top of the stack. This particular stack, which is a thin abstraction over the native JavaScript array, adds some other typical methods as well. When we're talking about a stack, we call the items in the stack "items" or "elements" because we don't really care what we're putting in the stack &mdash; numbers, strings, objects, etc. Without a generic type, we'd have to either create a new Stack class for each type we wanted to support, or we'd have to use `any`, which is an escape hatch from the type system and causes us to lose type safety. But our generic type parameter lets us do this:

```typescript
const numStack: Stack<number> = new Stack();
const stringStack: Stack<string> = new Stack();
```

Here we're passing in type arguments that tell TypeScript that `numStack` should only operate on numbers, and `stringStack` should only operate on strings. We use the same angle bracket syntax (`<number>`, `<string>`) for passing in type arguments as we did for defining type parameters. Now, if we try to pass in an incorrect type ...

```typescript
numStack.push('foo');
```

... TypeScript will throw an error:

    Argument of type '"foo"' is not assignable to parameter of type 'number'.

So what happens if we just ignore the type parameter? Let's try it:

```typescript
const anyStack = new Stack();
let myString: string;
anyStack.push('foo');
anyStack.push('bar');
const item = anyStack.pop();
myString = item; // Type 'unknown' is not assignable to type 'string'.
```

Here we created a stack without passing a type argument, and then we pushed to strings onto the stack. When we pop one of the strings off of the stack, does TypeScript know that it's a string? No, it doesn't. Because we didn't specify a type when we instantiated the class, TypeScript infers the type to be [unknown](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#new-unknown-top-type).

Our Stack class defines only one type parameter, `T`, but we're not limited in the number of type parameters we can define. Consider this Entry class:

```typescript
/**
 * A mapping of generic keys to generic values.
 */
export class Entry<K, V> {
  private key: K;
  private value: V;

  constructor(key: K, value: V) {
    this.key = key;
    this.value = value;
  }

  public getKey(): K {
    return this.key;
  }

  public getValue(): V {
    return this.value;
  }

  public toString(): string {
    return `${this.key}: ${this.value}`;
  }
}
```

In our class declaration, we define two type parameters, `K` and `V`. This lets us create a data structure that maps any type to any type. We can use the class like this:

```typescript
const numToStr: Entry<number, string> = new Entry(23, 'foo');
const strToStr: Entry<string, string> = new Entry('foo', 'bar');
const strToNum: Entry<string, number> = new Entry('foo', 23);
```

There's a subtle difference between the `Stack` and `Entry` methods that's worth considering. `Stack` doesn't make any assumptions about the internals of the items it's operating on. You can push primitives or custom objects, and `Stack` will just work as expected. `Entry`, on the other hand, has a method, `toString`, that implicitly invokes `Object.prototype.toString()` on the `K` and `V` types. If these types are primitives, you'll get an informative string output:

```typescript
console.log(numToStr.toString()); // 23: foo 
```

But if your mapping involves an object your mileage may vary:

```typescript
interface SimpleObject {
  prop: unknown;
}

const myObj: SimpleObject = {
    prop: 'foo',
}

const objToString: Entry<SimpleObject, string> = new Entry(myObj, 'foo');
console.log(objToString.toString()); // [object Object]: foo 
```

Because `myObj` does not override `Object.prototype.toString()`, it's string representation is `[object Object]`. That's not particularly helpful. We could refactor our code to create a `SimpleObject` class and then override `toString` on the prototype, but the larger point here is that generic types are not magic. The TypeScript compiler will prevent you from accessing properties that might not exist, but it can't guarantee that the runtime behavior will be what the user expects for any possible type.

## Generic functions

The syntax for a generic function looks similar to a generic class:

```typescript
/**
 * Returns the largest item in the array, or the first item, if all objects are equal.
 */
function getLargest<T>(arr: T[]): T {
  let largest: T = arr[0];
  arr.forEach((item) => {
    if (item > largest) {
      largest = item;
    }
  });
  return largest;
}
```










The type variable represents a type instead of a value. Later, you can pass in a type argument to tell the compiler what the type should be. In many cases, TypeScript will also be able to infer the value of the generic type without an explicit type argument.

You can define a generic type parameter using a type variable in angle brackets, e.g. `<T>`. You can explicitly define the type when instantiating a class or calling a function. If you don't, the compiler will try to use type argument inference.

* A function can be generic.
* A class can be generic.
* An interface can be generic.
* When a class is instantiated or a function invoked, the type parameter can be specified.
* An array data structure is basically a built-in generic type.

* TypeScript throws a compile-time error if you try to use a generic type in a non-generic way.
* Type parameters
* Particularly useful for data structures like a stack or a queue, i.e. for collections, which are often implemented with an array. The operations on the collection can operate on any type. For example, queueing and dequeueing items from a queue should be the same regardless of the item type.
* A type parameter serves as a placeholder for a type that is declared when a class is instantiated. In the case of a generic function, the type can often be inferred when the function is invoked.
* Generics make code more reusable.
* You can constrain a type parameter using the `extends` key word and an interface. Constraining a type parameter lets you make assumptions about that type. For example, let's say that we have a function `getAge` that can calculate a person's current age from their date of birth. We'd like to be able to use this on different kinds of people.

## Additional resources

* [C# Programming Guide: Constraints on type parameters](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/constraints-on-type-parameters)
* [C# Programming Guide: Generics](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/)
* [C# Programming Guide: Generic Classes](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/generic-classes)
* [C# Programming Guide: Generic Type Parameters](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/generic-type-parameters)
* [Generics in Java](https://en.wikipedia.org/wiki/Generics_in_Java)
* [Generic programming](https://en.wikipedia.org/wiki/Generic_programming)
* [The Java Tutorials: Why Use Generics?](https://docs.oracle.com/javase/tutorial/java/generics/why.html)
* [MDN: JavaScript data types and data structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
* [TypeScript Handbook: Generics](https://www.typescriptlang.org/docs/handbook/generics.html)
