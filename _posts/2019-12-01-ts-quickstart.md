---
title: Set up a TypeScript project
category: TypeScript
---

*Last updated: December 4, 2019*

This post explains how to set up a basic TypeScript project. The first section provides some context on why you might want to use TypeScript. If you just want to get started writing code, feel free to skip right to "Setting up the project."

## Why TypeScript?

Using TypeScript for a Node.js project takes more initial set up than using the vanilla JavaScript supported by the Node runtime. So why would you want to use it?

JavaScript is a dynamically typed language. Any type checking that gets done in JavaScript gets done at runtime, and this can be a source of bugs. TypeScript provides static typing and analysis for JavaScript. When you run the TypeScript compiler on your source code, it can find potential runtime errors before your users do. TypeScript provides interfaces and type annotations to let you explicitly tell the compiler the types of values in your code. It also provides type inference, so that the compiler can "guess" what a type should be. Using this information, TypeScript can analyze your code and throw an error if, for example, you're passing a value that could be a string *or* a boolean to a function that is expecting only a string.

In addition to type safety, TypeScript provides support for next-gen versions of JavaScript. In fact, TypeScript is actually a superset of JavaScript. Any valid JavaScript program is also a valid TypeScript program (though your configuration might prevent vanilla JavaScript syntax from compiling without errors). The [TypeScript compiler options](https://www.typescriptlang.org/docs/handbook/compiler-options.html) let you include libraries for ES6, ES2015, ES2016, ES2017, ESNext, and other proposed versions of ECMAScript. You can use features from these specifications in your source code, and then you can compile that code to a more widely supported ECMAScript target like ES3 or ES5. There are other tools available to do this, notably [Babel](https://babeljs.io/). But with TypeScript, you don't need to include Babel in your tool chain (though [TypeScript does support Babel 7](https://devblogs.microsoft.com/typescript/typescript-and-babel-7/)).

There are many other considertions around tooling, text editors, legacy code bases, and so on. But the basic tradeoff is that TypeScript gives you type safety and advanced language features at the cost of configuration and a higher learning curve for JavaScript developers working on a TypeScript project for the first time.

Now let's see how to create a bare-bones TypeScript project.

## Setting up the project

To complete the steps below, you need to [install Node.js](https://nodejs.org/en/download/). (There's a [node formula for Homebrew](https://formulae.brew.sh/formula/node), also.)

1. Create a directory for your project: `mkdir <my-app>`
1. Create a new npm package: `cd <my-app> && npm init -y`
1. Install TypeScript: `npm install typescript --save-dev`
1. Initialize a **tsconfig.json**: `npx tsc --init`
1. Create a source directory and a TypeScript file: `mkdir src && cd src && touch example.ts`
1. Add the following code to **src/example.ts**:

   ```javascript
   interface Person {
     firstName: string;
     lastName: string;
   }

   function greeter(person: Person) {
     return "Hello, " + person.firstName + " " + person.lastName;
   }

   const user = { firstName: "Bob", lastName: "Bobberson" };

   console.log(greeter(user));
   ```

1. Update the scripts section of **package.json** to look like this:

   ```json
   "scripts": {
     "build": "tsc"
   },
   ```

1. Open **tsconfig.json** and make the following changes:
  * Under `"compilerOptions"`, uncomment `"lib"` and set it to `[ "es2015", "dom" ]`.
  * Uncomment `"outDir"` and point it at a **dist** directory: `"outDir": "./dist"`.
  * Add the following `"include"` and `"exclude"` sections as siblings of "compilerOptions":

   ```json
   "include": [
        "src/**/*"
    ],
   "exclude": [
     "node_modules",
     "dist"
   ]
   ```

   Now the build will only look for TypeScript files in the the **src** directory, and it will ignore any TypeScript files in **node_modules** and **dist**.
1. (Optional) If you're using Git, you should ignore the **dist** and **node_modules** directories, ensuring that only your source files are under version control.
1. Run the TypeScript build: `npm run build`. You'll find a transpiled file at **dist/example.js**. If you open the file, you'll see that the interface has been removed from the output, as expected. Great! We've compiled TypeScript to JavaScript.

At this point, you should have a minimal TypeScript project. To learn how to add unit tests, see [Add tests to a TypeScript project]({% post_url 2019-12-02-ts-add-tests %}).