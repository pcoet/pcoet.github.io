# TypeScript quickstart

This tutorial shows you how to set up a TypeScript project for backend (i.e.
Node.js) development. There are many ways to set up a TypeScript project, and
this tutorial offers opinionated guidance about linting, testing, formatting,
and compiling tools. The goal is to leave you with a useful setup for
TypeScript development. You should swap out tools and adapt the configuration
based on the the needs of your project.

To complete this tutorial, you need to have Node.js installed. To install
Node.js, follow the instuctions at
[Download Node.js](https://nodejs.org/en/download).

## Create an npm package

Make a directory for your project and change into it:

    mkdir tsproj && cd tsproj

Initialize an npm package:

    npm init -y

You should see a new `package.json` file in your project directory. In this
file, update `"scripts"` so it looks like this:

```javascript
"scripts": {
  "clean": "rm -rf dist",
  "lint": "eslint ./src",
  "check": "tsc --noEmit",
  "format": "prettier . --write",
  "test": "jest",
  "compile": "swc src -d dist --strip-leading-paths",
  "build": "npm run clean && npm run format && npm run check && npm run lint && npm run test && npm run compile"
},
```

These scripts will become useful after you add and configure dependencies.

Also specify the module type, so that you can use ESM imports:

```javascript
"type": "module",
```

## Install dependencies

Install dependencies using the `--save-dev` flag:

    npm install --save-dev @eslint/js @swc/cli @swc/core @types/eslint__js @types/jest eslint jest prettier ts-jest typescript typescript-eslint

## Configure TypeScript

Create a `tsconfig.json` file and add the following content:

```javascript
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "NodeNext",
    "outDir": "./dist",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true
  }
}
```

Here you're using `"compilerOptions"` to configure the TypeScript compiler. To
learn more about TypeScript compiler options, see the
[TypeScript documentation](https://www.typescriptlang.org/tsconfig/).

Note that you're setting `"outDir"` to `"./dist"`. If you're planning to put
your project into version control using Git, you should add the `dist` directory
to your `.gitignore` file.

## Configure testing

Create a `jest.config.js` file and add the following content, which configures
[ts-jest](https://kulshekhar.github.io/ts-jest/):

```javascript
export default {
  preset: 'ts-jest',
  testEnvironment: 'node',
  transform: { '\\.[jt]sx?$': 'ts-jest' },
  moduleNameMapper: {
    '^(\\.{1,2}/.*)\\.js$': '$1', // map e.g. `../function.js` to `../function`
  },
  extensionsToTreatAsEsm: ['.ts'],
};
```

## Configure linting

Create an `eslint.config.js` file and add the following content:

```javascript
import eslint from '@eslint/js';
import tseslint from 'typescript-eslint';
import globals from 'globals';

export default tseslint.config(
  eslint.configs.recommended,
  ...tseslint.configs.recommended,
  ...tseslint.configs.stylistic,
  {
    languageOptions: {
      globals: {
        ...globals.node,
      },
    },
  },
);
```

Here you're configuring [eslint](https://eslint.org/) and
[typescript-eslint](https://typescript-eslint.io/).

## Configure code formatting

You already installed [Prettier](https://prettier.io/), which you can use to
format your code. Although you don't have to add any formatting rules, it's
useful to have a config file, in case you need it later.

Create a `.prettierrc` file and add the following content, which tells Prettier
to use single quotes:

```javascript
{
  "singleQuote": true
}
```

## Create a TypeScript source file

Make a `src` directory for your TypeScript code. (Several of the build scripts
in `package.json` expect the TypeScript code to be in the `src` directory.)

    mkdir src

Create a `utils.ts` file in `src` and add the following content:

```typescript
export function cube(x: number) {
  return x * x * x;
}
```

## Create a test

Make a `test` directory and create a `utils.test.ts` file in that directory. Add
the following content:

```typescript
import { cube } from '../src/utils.js';

describe('utils', () => {
  test('cube', () => {
    expect(cube(3)).toEqual(27);
  });
});
```

Here you use the Jest functions `describe`, `test`, and `expect` to validate
the output of `cube`.

## Test the setup

At this point, all of the build scripts should work. You can test them
one by one.

### `npm run compile`

After running `compile`, you should see a new `dist` directory, which will
contain the transpiled JavaScript for your project. For this project, we're
using [SWC](https://swc.rs/) to compile TypeScript. It's significantly faster
than the `tsc` command. To learn more, see
[Migrating from tsc](https://swc.rs/docs/migrating-from-tsc).

### `npm run check`

The `check` command uses `tsc --noEmit` to type-check the TypeScript source
files without transpiling them. SWC strips out TypeScript syntax without doing
any type checking, so we need to run `tsc` to take advantage of TypeScript type
safety.

### `npm run clean`

The `clean` command removes the `dist` directory and all of the JavaScript
output.

### `npm run test`

The `test` command runs the tests in `*.test.ts` files.

### `npm run lint`

This lints the TypeScript files in the `src` directory.

### `npm run format`

If Prettier finds any files in your project that don't match its formatting
rules, it fixes the formatting and overwrites the files.

### `npm run build`

`build` puts all of the other scripts together in a single command that cleans,
formats, type-checks, lints, tests, and compiles your TypeScript.

## Learn more

At this point, you have a fairly robust TypeScript environment for
Node.js development. Your `cube` function is a good example of how you could
develop a library, and you could also use this environment to develop a Node.js
application.

To learn more about TypeScript, check out the official
[TypeScript documentation](https://www.typescriptlang.org/docs/), and
particularly the
[TypeScript handbook](https://www.typescriptlang.org/docs/handbook/intro.html).

If you're interested in doing front-end develpment with TypeScript, you might
consider setting up your dev environment with [Vite](https://vite.dev/), which
[supports TypeScript](https://vite.dev/guide/features.html#typescript) and
includes several TypeScript templates for
[scaffolding your project](https://vite.dev/guide/#scaffolding-your-first-vite-project).
