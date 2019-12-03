---
title: Add linting to a TypeScript project
tags: [TypeScript, linting]
---

This post assumes that you've already [set up a TypeScript project]({% post_url 2019-12-01-ts-quickstart %}) and [created tests]({% post_url 2019-12-02-ts-add-tests %}).

TSLint was the standard TypeScript linter, but it's scheduled for deprecation in 2019, in favor of [TypeScript ESLint](https://github.com/typescript-eslint/typescript-eslint). So we'll use that instead.

1. Install dependencies: `npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin acorn --save-dev`.
1. In the project root, create **tsconfig.eslint.json** and add the following content:
   ```json
   {
     // extend your base config so you don't have to redefine your compilerOptions
     "extends": "./tsconfig",
     "exclude": [
       "node_modules",
       "dist"
     ]
   }
   ```
   Here we're creating a second config file for linting. This is necessary because, in the previous tutorial, we excluded test files from transpilation in **tsconfig.json**. And now we want to override that exclude in tsconfig.eslint.json, so that we can lint those test files. Basically, we want to lint them but not transpile them. 
1. In the project root, create an **.eslintrc.json** config file and add the following content:
   
   ```json
   {
     "parser": "@typescript-eslint/parser",
     "parserOptions": {
       "tsconfigRootDir": ".",
       "project": "tsconfig.eslint.json"
     },
     "plugins": [
       "@typescript-eslint"
     ],
     "extends": [
       "eslint:recommended",
       "plugin:@typescript-eslint/eslint-recommended",
       "plugin:@typescript-eslint/recommended",
       "plugin:@typescript-eslint/recommended-requiring-type-checking"
     ]
   }
   ```

   In `parserOptions.project`, we point to the config file we just created. In the `"extends"` section, we enable linting rules. There are other possible configurations. To learn more, see the [TypeScript ESLint Parser README](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/parser/README.md) and the [ESLint Plugin TypeScript README](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/README.md).
1. In **package.json**, add a linting script:

   ```json
   "scripts": {
     ...
     "lint": "eslint **/*.ts"
   },
   ```

1. Now run the linter: `npm run lint`. You should see a warning about a "Missing return type on function" in **example.ts**. Yay! We have linting. If you fix the error and run the script again, the linter should exit successfully. 