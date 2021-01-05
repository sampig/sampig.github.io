---
layout: post
title: "Introduction to ESLint"
date: 2020-12-20 01:05:00 +0200
category: tutorial
tagline: ""
tags: [JavaScript, ESLint]
abstract : "Learning ESLint: an introduction."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Installation and Usage](#installation-and-usage)
* [Configuration](#configuration)
  - [Rules](#rules)
  - [Other Configurations](#other-configurations)
* [Additional Plugins](#additional-plugins)
* [References](#references)


# Introduction

ESLint is a static code analysis tool to find and fix problems in JavaScript code.

1. ESLint statically analyzes code to quickly find problems. ESLint is built into most text editors and we can run ESLint as part of continuous integration pipeline.
2. Many problems ESLint finds can be automatically fixed. ESLint fixes are syntax-aware so we won't experience errors introduced by traditional find-and-replace algorithms.
3. Pre-process code, use custom parsers, and write own rules that work alongside ESLint's built-in rules. We can customize ESLint to work exactly the way we need it for our project.


# Installation and Usage

Install ESLint using `npm` or `yarn`:
```
npm install eslint --save-dev

yarn add eslint --dev
```

Set up the configuration file `package.json`, and the easiest way to do that is to use the `--init` flag:
```
npx eslint --init

yarn run eslint --init
```

Then we can run ESLint on any file or directory like this:
```
npx eslint filename.js

yarn run eslint filename.js

eslint filename.js
```


# Configuration

After running `eslint --init`, a `.eslintrc.{js,yml,json}` configuration file will be generated in the project directory. The content inside looks like:

```json
{
  "extends": [
    "eslint:recommended"
  ],
  "rules": {
    "semi": ["error", "always"],
    "quotes": ["error", "single"]
  }
}
```

With the `extends` line `"eslint:recommended"`, all of the rules marked with check mark on the [rules](https://eslint.org/docs/rules/){:target="_blank"} page will be turned on.

## Rules

The `rules` section defines the rules for the projects. The format of each rule is `name` and an array of its settings (values and additional configurations). The values are:
- "off" or 0 - turn the rule off
- "warn" or 1 - turn the rule on as a warning (doesn't affect exit code)
- "error" or 2 - turn the rule on as an error (exit code is 1 when triggered)

There are many other rules which can be found in [rules](https://eslint.org/docs/rules/){:target="_blank"}.

Rules can also be set inside of a file using comments like:

```javascript
/* eslint quotes: ["error", "single"], curly: 2 */
```

Rules can also be disabled for line(s) in file.

Disable all rules:

```javascript
/* eslint-disable */

/* eslint-enable */
```

Disable a specific rule:

```javascript
/* eslint-disable no-alert, no-console */

/* eslint-enable no-alert, no-console */
```

Disable single line:

```javascript
alert('foo'); // eslint-disable-line

// eslint-disable-next-line
alert('foo');

alert('foo'); // eslint-disable-line no-alert

// eslint-disable-next-line no-alert
alert('foo');
```

We can even disable rules for a group of files. An example:

```javascript
{
  "rules": {...},
  "overrides": [
    {
      "files": ["*-test.js","*.spec.js"],
      "rules": {
        "no-unused-expressions": "off"
      }
    }
  ]
}
```

## Other Configurations

Other configurations includes:

- Specify parser options: ecmaVersion, sourceType and ecmaFeatures.
- Specify parser: [esprima](https://www.npmjs.com/package/esprima){:target="_blank"}, [babel eslint parser](https://www.npmjs.com/package/@babel/eslint-parser){:target="_blank"} and [typescript eslint parser](https://www.npmjs.com/package/@typescript-eslint/parser){:target="_blank"}. (For example, install a parser with `yarn add --dev babel-eslint`.)
- Specify environments such as browser, node, commonjs, etc.
- Configure plugins.
- ...


# Additional Plugins

There are many plugins for different JavaScript libraries, like:
1. [ESLint-plugin-React](https://github.com/yannickcr/eslint-plugin-react){:target="_blank"}: React specific linting rules for ESLint.
2. [ESLint plugin for React Native](https://github.com/Intellicode/eslint-plugin-react-native){:target="_blank"}: React Native specific linting rules for ESLint.
3. [ESLint plugin Angular](https://github.com/EmmanuelDemey/eslint-plugin-angular){:target="_blank"}: ESLint rules for angular project with checks for best-practices, conventions or potential errors.

Install:
```
npm install --save-dev eslint-plugin-react

npm install --save-dev eslint-plugin-react-native

npm install --save-dev eslint-plugin-angular

yarn add --dev eslint-plugin-react

yarn add --dev eslint-plugin-react-native

yarn add --dev eslint-plugin-angular
```

When using these plugins, do NOT forget to update the configuration files `package.json` and `.eslintrc*`. The details can be found their documentations.


# References

1. [ESLint - Pluggable JavaScript linter](https://eslint.org/){:target="_blank"}
2. [ESLint-plugin-React](https://github.com/yannickcr/eslint-plugin-react){:target="_blank"}
3. [ESLint plugin for React Native](https://github.com/Intellicode/eslint-plugin-react-native){:target="_blank"}
4. [ESLint plugin Angular](https://github.com/EmmanuelDemey/eslint-plugin-angular){:target="_blank"}
