---
title: Add tests to a TypeScript project
tags: [TypeScript, testing]
---

This post assumes that you've already [set up a TypeScript project]({% post_url 2019-12-01-ts-quickstart %}). Now we'll add unit tests to the project. [Jest](https://jestjs.io/) is the go-to framework for JavaScript projects at the moment, so we'll use that, and we'll also use [ts-jest](https://kulshekhar.github.io/ts-jest/) so that we can test our TypeScript files before they're transpiled to JavaScript.

1. In the root of your project, install the Jest and ts-jest dependencies: `npm install --save-dev jest typescript ts-jest @types/jest`.
1. Create a Jest config file: `npx ts-jest config:init`. You should see a **jest.config.js** file in your root directory. If you open the file, you'll see that the preset is set to `'ts-jest'`. This is what we want.
1. Add the following to the `"scripts"` section in your package.json: `"test": "jest"`.
1. We're going to write unit tests in TypeScript, and we don't want those to be transpiled, so we need to tell TypeScript to ignore them. Open **tsconfig.json** and add `"**/*.test.ts"` to the `"exclude"` list. Also, under `"compilerOptions"`, un-comment `"lib"` and set it to `[ "es2017", "dom" ]`.
1. Now we'll add TypeScript-ified versions of the example files from the [Jest getting started guide](https://jestjs.io/docs/en/getting-started.html). Create a file called **sum.ts** and add the following:

   ```javascript
   export const sum = (a: number, b: number): number => {
     return a + b;
   }
   ```

1. Create a file called **sum.test.ts** and add the following:

   ```javascript
   import { sum } from './sum';

   test('adds 1 + 2 to equal 3', () => {
     expect(sum(1, 2)).toBe(3);
   });
   ```

1. Run `npm run test`. You should see your test pass in the console output.
1. Run `npm run build`. The **sum.ts** file will be transpiled into **dist** as **sum.js**, and the test will not be transpiled.