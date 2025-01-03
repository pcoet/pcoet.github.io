---
draft: false
date: 2019-12-03
categories:
  - TypeScript
---

# Add linting to a TypeScript project

*Last updated: January 1, 2020*

This post assumes that you've already [set up a TypeScript project](ts-quickstart.md) and [created tests](ts-add-tests.md).

TSLint was the standard TypeScript linter, but it's scheduled for deprecation in 2019, in favor of [TypeScript ESLint](https://github.com/typescript-eslint/typescript-eslint). So we'll use that instead.

Using ESLint for TypeScript is a little bit more complicated than using it for vanilla JavaScript, because ESLint and TSLint both parse source code into abstract syntax trees (ASTs), but those trees will differ. This is why, in the configuration below, we use both the `eslint:recommended` rules and the `@typescript-eslint/eslint-recommended` rules &mdash; we need to have a TypeScript-ified version of the ESLint recommendations. Anyway, if you use the configuration below, you shouldn't need to worry about discrepancies in the syntax or the rules.

## Configure linting

1. Install dependencies: `npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin acorn --save-dev`
1. In the project root, create **tsconfig.eslint.json** and add the following content:
   ```json
   {
     "extends": "./tsconfig",
     "exclude": [
       "node_modules",
       "dist"
     ]
   }
   ```
   Here we're creating a second config file for linting. This is necessary because, in the previous tutorial, we set up our **tsconfig.json** to exclude test files from transpilation. And now we want to override that exclude in **tsconfig.eslint.json**, so that we can lint those test files. Basically, we want to lint them but not transpile them.
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

   In `parserOptions.project`, we point to the config file we just created. In the `"extends"` section, we enable linting rules. There are other possible configurations. To learn more, see the docs for [TypeScript ESLint Parser](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/parser/README.md) and [ESLint Plugin TypeScript](https://github.com/typescript-eslint/typescript-eslint/blob/master/packages/eslint-plugin/README.md).
1. In **package.json**, add a linting script:

   ```json
   "scripts": {
     ...
     "lint": "eslint . --ext .ts"
   },
   ```

## Lint!

Now run the linter: `npm run lint`. You should see a warning about a "Missing return type on function" in **example.ts**. Yay! We have linting. If you fix the error (great practice if you're learning TypeScript!) and run the script again, the linter should exit successfully.

## (Optional) Add airbnb

You may also want to add `eslint-config-airbnb-typescript` to your project. To add the airbnb rules, [follow these steps](https://www.npmjs.com/package/eslint-config-airbnb-typescript#i-use-eslint-config-airbnb-base-no-react-support).

## (Optional) Enable ESLint in VS Code

If you're using VS Code, you'll probably want to enable [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint). This will give you linting intellisense in the editor, so you don't have to run the linter to get feedback.

## Next steps

You now have a simple TypeScript project set up. Here are some things you could do next:

  1. If you're creating a library, you're already off to a pretty good start. Get rid of the example files and start writing useful code.
  1. If you want to set up a static web site, you might consider using webpack. The [TypeScript guide](https://webpack.js.org/guides/typescript/) will help you set up a TypeScript webpack project, and then you can add testing and linting as described in these posts.
  1. [Express](https://expressjs.com/) is a popular Node.js server. You could add it to this project and then stand up a server-side rendered web app or a web service. [This article](https://medium.com/javascript-in-plain-english/typescript-with-node-and-express-js-why-when-and-how-eb6bc73edd5d) provides instructions for setting up a TypeScript Express project (and also a nice perspective on why TypeScript is worth using).
  1. If you want to create a TypeScript React application, you can follow [these instructions](https://create-react-app.dev/docs/adding-typescript/).