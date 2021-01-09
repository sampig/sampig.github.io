---
layout: post
title: "Introduction to Jest"
date: 2020-12-25 15:55:00 +0200
category: tutorial
tagline: ""
tags: [JavaScript, Test, Jest]
abstract : "Learning Jest: an introduction."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Installation and Usage](#installation-and-usage)
* [Additional Configuration](#additional-configuration)
  - [Using Babel](#using-babel)
  - [Using TypeScript](#using-typescript)
* [Advanced Practice](#advanced-practice)
  - [Using Matchers](#using-matchers)
  - [Setup and Teardown](#setup-and-teardown)
  - [Mock Functions](#mock-functions)
  - [UI Components Testing](#ui-components-testing)
  - [Snapshot Testing](#snapshot-testing)
  - [DOM Testing](#dom-testing)
* [More Practices](#more-practices)
* [References](#references)


# Introduction

Jest is a delightful JavaScript Testing Framework with a focus on simplicity. It works with projects using: Babel, TypeScript, Node, React, Angular, Vue and more.

1. Jest is easy to configure.
2. Jest provides snapshots which make tests keep track of large objects with ease.
3. Tests are running in parallel.
4. Jest can generate code coverage.
5. Jest uses a custom resolver for imports in tests, making it simple to mock any object outside of test's scope.


# Installation and Usage

Install Jest using `npm` or `yarn`:
```
npm install --save-dev jest

yarn add --dev jest
```

After installing, update the configuration `package.json`:
```json
{
  "scripts": {
    "test": "jest"
  }
}
```
If `jest` is not in path, try with `"test": "node_modules/.bin/jest"`.

Assuming that there is a js file `sum.js` with a function:
```javascript
function sum(a, b) {
  return a + b;
}
module.exports = sum;
```

Then create a unit test file `sum.test.js` for the function:
```javascript
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

Finally, run `yarn test` or `npm run test` and Jest will print this message:
```
PASS  ./sum.test.js
✓ adds 1 + 2 to equal 3 (5ms)
```


# Additional Configuration

## Using Babel

In order to use [Babel](https://babeljs.io/){:target="_blank"}, install the required dependencies:
```
yarn add --dev babel-jest @babel/core @babel/preset-env
```
Create a configuration file `babel.config.js` in the root of the project to configure Babel:
```javascript
module.exports = {
  presets: [['@babel/preset-env', {targets: {node: 'current'}}]],
};
```

## Using TypeScript

Jest supports TypeScript via Babel. Install the required dependency after installing Babel:
```
yarn add --dev @babel/preset-typescript
```
Add one preset in the array of presents: `'@babel/preset-typescript'`.


# Advanced Practice

## Using Matchers

Jest uses matchers to test values in different ways with `expect`.

1. With exact equality: `expect(expression).toBe(value)`, `expect(expression).toEqual(value)`, `expect(expression).not.toBe(value)`.
2. With boolean:
  - `toBeNull` matches only `null`
  - `toBeUndefined` matches only `undefined`
  - `toBeDefined` is the opposite of `toBeUndefined`
  - `toBeTruthy` matches anything that an if statement treats as true
  - `toBeFalsy` matches anything that an if statement treats as false
3. Comparing numbers: `toBeGreaterThan`, `toBeGreaterThanOrEqual`, `toBeLessThan`, `toBeLessThanOrEqual`.
4. Checking strings against regular expressions with `toMatch`.
5. Checking an array or a collection: `toContain`.
6. Testing exception: `toThrow`.

## Setup and Teardown

Jest provides some functions to deal with some work before or after tests including scoping. An example with full structure:

```javascript
beforeAll(() => console.log('0 - beforeAll'));
afterAll(() => console.log('0- afterAll'));
beforeEach(() => console.log('0 - beforeEach'));
afterEach(() => console.log('0 - afterEach'));
test('test 0', () => console.log('0 - test'));

describe('Scoped / Nested block 1', () => {
  beforeAll(() => console.log('1 - beforeAll'));
  afterAll(() => console.log('1 - afterAll'));
  beforeEach(() => console.log('1 - beforeEach'));
  afterEach(() => console.log('1 - afterEach'));
  test('test 1', () => console.log('1 - test'));
});

describe('Scoped / Nested block 2', () => {
  beforeAll(() => console.log('2 - beforeAll'));
  afterAll(() => console.log('2 - afterAll'));
  beforeEach(() => console.log('2 - beforeEach'));
  afterEach(() => console.log('2 - afterEach'));
  test('test 2', () => console.log('2 - test'));
});
```

## Mock Functions

Mock functions allow to test the links between code by erasing the actual implementation of a function, capturing calls to the function (and the parameters passed in those calls), capturing instances of constructor functions when instantiated with new, and allowing test-time configuration of return values.

There are two ways to mock functions: Either by creating a mock function to use in test code, or writing a [manual mock](https://jestjs.io/docs/en/manual-mocks){:target="_blank"} to override a module dependency.

It can be used to inject test values:
```javascript
const myMock = jest.fn();
console.log(myMock());
// > undefined

myMock.mockReturnValueOnce(10).mockReturnValueOnce('x').mockReturnValue(true);

console.log(myMock(), myMock(), myMock(), myMock());
// > 10, 'x', true, true
```

It can also mock modules:
```javascript
...
jest.mock('moduleName');
...
moduleName.funcName.mockResolvedValue(value);
...
```

## UI Components Testing

There are many JavaScript libraries or frameworks about UI components such React, Angular and VueJS. Jest also supports testing with these libraries.

For example, add Jest into an existing React project.

A dependency is required:
```
yarn add --dev react-test-renderer
```
And, modify the babel configuration file `babel.config.js`:
```javascript
module.exports = {
  presets: ['@babel/preset-env', '@babel/preset-react'],
};
```

Create a test for a React component:
```javascript
import React from 'react';
import renderer from 'react-test-renderer';
import MyReactComponent from './MyReactComponent';

test('MyReactComponent works', () => {
  const component = renderer.create(
    <MyReactComponent />,
  );
  let tree = component.toJSON();
  expect(tree).toMatchSnapshot();

  // manually trigger the callback
  tree.props.onMouseEnter();
  // re-rendering
  tree = component.toJSON();
  expect(tree).toMatchSnapshot();

  // manually trigger the callback
  tree.props.onMouseLeave();
  // re-rendering
  tree = component.toJSON();
  expect(tree).toMatchSnapshot();
});
```

## Snapshot Testing

Snapshot tests are a very useful tool whenever you want to make sure your UI does not change unexpectedly.

A typical snapshot test case renders a UI component, takes a snapshot, then compares it to a reference snapshot file stored alongside the test. The test will fail if the two snapshots do not match: either the change is unexpected, or the reference snapshot needs to be updated to the new version of the UI component.

The usage of it:
```javascript
expect(expression).toMatchSnapshot();
```

A snapshot file `testFilename.snap` will be generated if the test is run at the first time. And it needs to be updated if the component is changed.

## DOM Testing

If you don't want to use snapshot, you can try to use DOM to deal with the expected output.
Some libraries such as [Testing Library](https://testing-library.com/){:target="_blank"}, [Enzyme](https://enzymejs.github.io/enzyme/){:target="_blank"} and [React's TestUtils](https://reactjs.org/docs/test-utils.html) can be used to manipulate the rendered components.

Install testing=library for React test:
```
yarn add --dev @testing-library/react
```
A test example with testing-library:
```javascript
import React from 'react';
import {cleanup, fireEvent, render} from '@testing-library/react';
import MyReactComponent from './MyReactComponent';

// unmount and cleanup DOM after the test is finished.
afterEach(cleanup);

test('MyReactComponent works', () => {
  const {queryByLabelText, getByLabelText} = render(
    <MyReactComponent />,
  );

  expect(queryByLabelText(/off/i)).toBeTruthy();

  fireEvent.click(getByLabelText(/off/i));

  expect(queryByLabelText(/on/i)).toBeTruthy();
});
```


# More Practices

There are other configuration or plugins which are helpful.

Configure coverage, including coverage files, reporter formats and threshold:
```json
{
  "jest": {
    "preset": "...",
    "collectCoverageFrom": [
      "components/**/*.js",
      "!hooks/*.js",
      "!locales/*.js"
    ],
    "coverageReporters": [
      "text",
      "html"
    ],
    "coverageThreshold": {
      "global": {
        "branches": 50,
        "functions": 50,
        "lines": 50,
        "statements": 50
      }
    }
  }
}
```

The `transformIgnorePatterns` option can be used to specify which files shall be transformed by Babel. Many react-native npm modules unfortunately don't pre-compile their source code before publishing.
```json
{
  "jest": {
    "preset": "...",
    "transformIgnorePatterns": [
      "node_modules/(?!(react-native|my-project|react-native-button)/)",
      "/node_modules/otherExpression"
    ]
  }
}
```

Add Jest for expo project:
```
yarn add --dev jest-expo
```
Configure preset:
```
"jest": { "preset": "jest-expo" }
// or
"jest": { "preset": "jest-expo/universal" }
```

Jest even supports to mock implementation and create custom matchers.

If some code uses a method which JSDOM (the DOM implementation used by Jest) hasn't implemented yet, testing it is not easily possible. This is e.g. the case with window.matchMedia(). Jest returns TypeError: window.matchMedia is not a function and doesn't properly execute the test.
In this case, mocking `matchMedia` in the test file should solve the issue:
```javascript
Object.defineProperty(window, 'matchMedia', {
  writable: true,
  value: jest.fn().mockImplementation(query => ({
    matches: false,
    media: query,
    onchange: null,
    addListener: jest.fn(), // deprecated
    removeListener: jest.fn(), // deprecated
    addEventListener: jest.fn(),
    removeEventListener: jest.fn(),
    dispatchEvent: jest.fn(),
  })),
});
```


# References

1. [Jest - Delightful JavaScript Testing](https://jestjs.io/){:target="_blank"}
2. [Testing Library](https://testing-library.com/){:target="_blank"}
