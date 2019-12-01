---
title: Set up a TypeScript project
tags: [quickstart, Node, TypeScript, JavaScript]
---

This post explains how to set up a simple TypeScript project.

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

1. Update **package.json** to look like this:

   ```json
   "scripts": {
     "build": "tsc"
   },
  ```

1. Run the TypeScript build: `npm run build`. You'll see the transpiled file, **index.js**, beside the TypeScript source file. If you open **index.js**, you'll see that the interface has been removed from the output, as expected.

At this point, you may want to open **tsconfig.json** and configure `outDir` so that the TypeScript is built into its own directory. For example, you might set `outDir` to point at a "dist" directory. Then, if you're using Git, you can ignore the directory, ensuring that only your source files are under version control.