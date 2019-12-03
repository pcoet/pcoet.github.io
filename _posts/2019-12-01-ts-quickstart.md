---
title: Set up a TypeScript project
category: TypeScript
---

*Last updated: December 3, 2019*

This post explains how to set up a basic TypeScript project. To complete the steps below, you need to [install Node.js](https://nodejs.org/en/download/). (There's a [node formula for Homebrew](https://formulae.brew.sh/formula/node), also.)

1. Create a directory for your project: `mkdir <my-app>`
1. Create a new npm package: `cd <my-app> && npm init -y`
1. Install TypeScript: `npm install typescript --save-dev`
1. Initialize a **tsconfig.json**: `npx tsc --init`
1. Create a source directory and a TypeScript file: `mkdir src && cd src && touch example.ts`
1. Add the following code to example.ts:

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
  * Under `"compilerOptions"`, uncomment `"lib"` and set it to `[ "es2017", "dom" ]`.
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
1. Run the TypeScript build: `npm run build`. You'll find a transpiled file at **dist/index.js**. If you open the file, you'll see that the interface has been removed from the output, as expected.

At this point, you should have a minimal TypeScript project. To learn how to add unit tests, see [Add tests to a TypeScript project]({% post_url 2019-12-02-ts-add-tests %}).