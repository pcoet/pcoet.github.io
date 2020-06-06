---
title: Add tests to a TypeScript project
category: TypeScript
last_updated: February 1, 2019
---

This post assumes that you've already [set up a TypeScript project]({% post_url 2019-12-01-ts-quickstart %}). Now we'll add unit testing to the project. [Jest](https://jestjs.io/) is the go-to testing framework for JavaScript projects at the moment, so we'll use that. The [Jest API](https://jestjs.io/docs/en/api) includes global setup and testing methods (e.g. `afterAll`, `beforeEach`, `describe`) that should look familiar to users of other JavaScript testing frameworks like Jasmine and Mocha.

Our source code is written in TypeScript, so we'll also use [ts-jest](https://kulshekhar.github.io/ts-jest/), a TypeScript preprocessor that will let us do type-checking at test time. To learn more about Jest support for TypeScript, see [the Jest docs](https://jestjs.io/docs/en/getting-started#using-typescript) and [the Jest blog](https://jestjs.io/blog/2019/01/25/jest-24-refreshing-polished-typescript-friendly#typescript-support).

## Installing Jest

1. In the root of your project, install Jest and related dependencies: `npm install --save-dev jest ts-jest @types/jest`
1. Create a Jest config file: `npx ts-jest config:init`

   You should see a **jest.config.js** file in your root directory. If you open the file, you'll see that the preset is `'ts-jest'`. This is what we want.
1. In your **package.json**, add a test script:

   ```json
   "scripts": {
     ...
     "test": "jest"
   },
   ```

1. We're going to write unit tests in TypeScript, and we don't want those to be transpiled, so we need to tell TypeScript to ignore them. Open **tsconfig.json** and add `"**/*.test.ts"` to the `"exclude"` list.

## Adding a test

When we set up our TypeScript project, we created an example file with a function, `isOldTimey`. Let's test it. 

First, we'll create a file for our test: **src/example.test.ts**.

Now let's add the following content:

```javascript
import { Album, Genre, isOldTimey } from './example';

describe('isOldTimey', () => {
  test('returns false when the album year is greater than or equal to 1950', () => {
    const album: Album = {
      artist: 'John Lee Hooker',
      title: 'Endless Boogie',
      genre: Genre.Blues,
      year: 1971,
    };
    expect(isOldTimey(album)).toEqual(false);
  });

  test('returns false when the album genre is jazz', () => {
    const album: Album = {
      artist: 'Benny Goodman',
      title: 'Swing into Spring',
      genre: Genre.Jazz,
      year: 1941,
    };
    expect(isOldTimey(album)).toEqual(false);
  });

  test('returns true when the album year is less than 1950 and the album genre is folk', () => {
    const album: Album = {
      artist: 'Woody Guthrie',
      title: 'Dust Bowl Ballads',
      genre: Genre.Folk,
      year: 1940,
    };
    expect(isOldTimey(album)).toEqual(true);
  });
});
```

Here we have three tests to make sure that our function returns the expected results. Note that we're using both the `Album` interface and the `Genre` enum in our tests. We're making use of TypeScript.

Let's run our test: `npm run test`. 

You should see the successful test results in the console output. Note: If there's an error indicating that Jest `describe` can't be found, you may be need to open **jest.config.js** and set `testEnvironment` to `jsdom`. If you're using an older version of Node, you may encounter problems when you try to use `import` with `testEnvironment: node`.

While we're at it, let's trying building again: `npm run build`. If you look in the **dist** dir, you'll see that **example.js** is there, as expected, but the test is not. We've excluded the test from being transpiled to the build output, as we should.

Great, now we have unit testing! Finally, we'll [add linting]({% post_url 2019-12-03-ts-add-linting %}).