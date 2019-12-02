---
title: Set up a TypeScript project
tags: [quickstart, Node, TypeScript, JavaScript]
---

*Last updated: December 2, 2019*

This post explains how to set up a basic TypeScript project. To complete the steps below, you need to [install Node.js](https://nodejs.org/en/download/). (There's a [node formula for Homebrew](https://formulae.brew.sh/formula/node), also.)

1. Create a directory for your project: `mkdir <my-app>`
1. Create a new npm package: `cd <my-app> && npm init -y`
1. Install TypeScript: `npm install typescript --save-dev`
1. Initialize a tsconfig.json: `npx tsc --init`
1. Create a TypeScript file: `touch index.ts`
1. Add the following code to index.ts:

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

1. Update the scripts sction of **package.json** to look like this:

   ```json
   "scripts": {
     "build": "tsc"
   },
   ```

1. Open **tsconfig.json**, un-comment `"outDir"`, and point it at a **dist** directory: `"outDir": "./dist"`. Also, add an "exclude" section as a sibling of "compilerOptions", and exclude **node_modules** and **dist**:

   ```json
   "exclude": [
     "node_modules",
     "dist"
   ]
   ```

1. (Optional) If you're using Git, you should ignore the **dist** and **node_modules** directories, ensuring that only your source files are under version control.
1. Run the TypeScript build: `npm run build`. You'll find a transpiled file at **dist/index.js**. If you open the file, you'll see that the interface has been removed from the output, as expected.

At this point, you should have a minimal TypeScript project. To learn how to add unit tests, see [Add tests to a TypeScript project]({% post_url 2019-12-02-ts-add-tests %}).