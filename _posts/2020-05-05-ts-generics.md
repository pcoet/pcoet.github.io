---
title: Using TypeScript generics
category: TypeScript
---

To help make code more reusable, TypeScript provides generics. If you're a Java or C# developer, you're probably already familiar with generic types. If not, this post should help you understand what they are and how to use them.

JavaScript defines [primitive](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) types (e.g. String, Number, Boolean), the [null](https://developer.mozilla.org/en-US/docs/Glossary/null) type, an [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) type, and a [Function](https://developer.mozilla.org/en-US/docs/Glossary/Function) type derived from Object. TypeScript provides an additional generic type, which represents a range of types.

You can use the generic type to make functions, classes, or interfaces operate over the set of all types or a subset of types. To define a generic type, you use a type variable in angle brackets: `<T>`. By convention, `T` is often used for the type parameter, but the variable name can be anything.

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

Why would we want to make this class generic? Well, let's think about a stack data structure. We use a stack as an interface to a collection of items. A stack lets you push an element onto the end of the collection (i.e. the top of the stack) and pop (i.e. remove and return) an element from the top of the stack. This particular stack, which is a thin abstraction over the native JavaScript array, adds some other methods as well. When we're talking about a stack, we call the objects in the stack "items" or "elements" because we don't really care what we're putting in the stack &mdash; numbers, strings, objects, etc. Without a generic type, we'd have to either create a new `Stack` class for each type we wanted to support, or we'd have to use `any`, which is an escape hatch from the type system and causes us to lose type safety. But with a generic type parameter, we can do this:

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

Here we created a `Stack` without passing a type argument, and then we pushed two strings onto the stack. When we pop one of the strings off of the stack, does TypeScript know that it's a string? No, it doesn't. Because we didn't specify a type when we instantiated the class, TypeScript infers the type to be [unknown](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#new-unknown-top-type).

Our `Stack` class defines only one type parameter, `T`, but we're not limited in the number of type parameters we can define. Consider this `Entry` class:

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

But if your mapping involves an object, your mileage may vary:

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

Because `myObj` does not override `Object.prototype.toString()`, it's string representation is `[object Object]`. That's not particularly helpful. We could override `toString` on the prototype, but for now let's just note that generic types are not magic. The TypeScript compiler will prevent you from accessing properties that might not exist, but it can't guarantee that the runtime behavior will be what the user expects for any possible type.

## Generic functions

The syntax for a generic function looks similar to a generic class. You define one or more type parameters in the function declaration, as shown in the `getLargest` function below:

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

We define our generic type, `T`, in angle brackets, and then use it to type both the function parameter and the return value. The function expects an array of `T`s as an argument, and it will return a `T` as well. It assigns the first item in the array to a `largest` variable and then iterates over every item in the array, comparing it to `largest`. If the current item is larger, we assign that item to `largest`, and when we're done iterating, we return `largest`. Here's an example of using the function:


```typescript
const arr = [5, 117, 19, 23];
const largest = getLargest(arr);
console.log(largest); // 117
```

The `getLargest` function works as you'd expect with numbers and strings. But what if you pass in a custom object? After all, our type variable, `T`, doesn't place any constraints on the types we can use. Let's create a test class and see:

```typescript
class Member {
  firstName: string;
  lastName: string;
  dob: Date;
  id: number;

  constructor(firstName: string, lastName: string, dob: Date, id: number) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.dob = dob;
    this.id = id;
  }
}
```

The `Member` class stores some basic personal information. To make it useful, we'd probably want to add getters and setters and other methods, but this is fine for current purposes. Let's create an array of members:

```typescript
const mick = new Member('Mick', 'Jagger', new Date(1943, 7, 26), 111);
const charlie = new Member('Charlie', 'Watts', new Date(1941, 6, 2), 112);
const ronnie = new Member('Ronnie', 'Wood', new Date(1947, 6, 1), 113);
const keith = new Member('Keith', 'Richards', new Date(1943, 12, 18), 114);

const members = [mick, charlie, ronnie, keith];
```

(By coincidence, our members share names with the members of a certain rock and roll band which is superior to the Beatles.) Now, what happens when we pass `members` to `getLargest`? 

```typescript
const largest = getLargest(members);
console.log(largest); // { "firstName": "Mick", "lastName": "Jagger", "dob": "1943-08-26T07:00:00.000Z", "id": 111 }
```

We get back `mick`, for the simple reason that `mick` is the first item in the `members` array. Our `getLargest` function initially assigns the first item to `largest`. Then, as the function iterates over the array, comparing items, it fails to find a "larger" item than `mick`. This is because JavaScript uses [Object.prototype.valueOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf) to test if one object is greater than another. In order to make our `member` objects comparable, we need to override `valueOf` and provide a primitive value for comparison. Here's how we can do that:

```typescript
Member.prototype.valueOf = function getOverrideValue(): string {
  return this.lastName;
};
```

Now, when `getLargest` iterates over members, it will compare their `lastName` property. We could just as well have decided that "largest" means something else, like the largest `id`. When we run the function on `members`, it returns `ronnie`, which has the largest `lastName` string. 

That works, but it's not using the type system to best advantage. If we don't remember to override `valueOf` on any non-primitive type that we use with `getLargest`, we're likely to get a result that doesn't make sense. A better way to handle this scenario would be to constrain the type, using the `extends` keyword and an interface. 

Using a TypeScript interface, we can define the shape of an object. We can then use the interface to constrain the type of a function. This let's us know something in advance about the type the function is operating on. Say, for example, we wanted to find the oldest member in an array of `Member` objects. One way to do that, not using a constrained generic type, would be like this: 

```typescript
function getOldest(arr: Member[]): Member {
  let oldest: Member = arr[0];
  arr.forEach((born) => {
    if (born.dob < oldest.dob) {
      oldest = born;
    }
  });
  return oldest;
}

const oldestMember = getOldest(members);
console.log(oldestMember); // { "firstName": "Charlie", "lastName": "Watts", "dob": "1941-07-02T08:00:00.000Z", "id": 112 } 
```

This works. But our `getOldest` function can only operate on `Member` objects. Maybe we'd like to find the oldest item in arrays of other types, too. This is where we need a constrained generic type. If we look at the function body, our function is only making one assumption about the objects in the array &mdash; each object has to have a `dob` property that can be compared. We can define that shape using an interface:

```typescript
interface HasBirthday {
  dob: Date;
}
```

And now we can use that interface to constrain a generic type parameter in `getOldest`:

```typescript
function getOldest<T extends HasBirthday>(arr: T[]): T {
  let oldest: T = arr[0];
  arr.forEach((born) => {
    if (born.dob < oldest.dob) {
      oldest = born;
    }
  });
  return oldest;
}
```

This will work as expected for a `Member` array, and it will also work for an array of any other type as long as the items have a `dob: Date` property. TypeScript interfaces are based on duck typing, meaning that an object that has a shape defined by an interface implicitly extends that interface. To learn more about how interfaces work, see [Interfaces](https://www.typescriptlang.org/docs/handbook/interfaces.html) in the official TypeScript docs.

## Things to know

Here are a few things to keep in mind when you're working with TypeScript generics:

* Functions, classes, and interfaces can all be generic.
* TypeScript throws a compile-time error if you try to use a generic type in a non-generic way, e.g. accessing a property that might not exist.
* You can define a generic type parameter using a type variable in angle brackets, e.g. `<T>`. You can explicitly define the type when instantiating a class or calling a function. If you don't, the compiler will try to infer the value of the generic type.
* You can constrain a type parameter using the `extends` keyword and an interface. Constraining a type parameter lets you make assumptions about that type.

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
