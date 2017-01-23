# Serverless Jest Plugin

[![Build Status](https://travis-ci.org/SC5/serverless-jest-plugin.svg?branch=master)](https://travis-ci.org/SC5/serverless-jest-plugin)

A Serverless Plugin for the [Serverless Framework](http://www.serverless.com) which
adds support for test-driven development using [jest](https://facebook.github.io/jest/)

**THIS PLUGIN REQUIRES SERVERLESS V1.0 OR NEWER!**

More familiar with Mocha? Use [serverless-mocha-plugin](https://github.com/sc5/serverless-mocha-plugin).

## Introduction

This plugins does the following:

* It provides commands to create and run tests manually
* It provides a command to create a function, which automatically also creates a test

## Installation

In your service root, run:

```bash
npm install --save-dev serverless-jest-plugin
```

Add the plugin to `serverless.yml`:

```yml
plugins:
    - serverless-jest-plugin
```

## Usage

### Creating functions

Functions (and associated tests) can be created using the command

```
sls create function -f functionName --handler handler
```
 
e.g.

```
sls create function -f myFunction --handler functions/myFunction/index.handler
```

creates a new function `myFunction` into `serverless.yml` with a code template for
the handler in `functions/myFunction/index.js` and a Javascript function `module.exports.handler` 
as the entrypoint for the Lambda function. A test template is also created into `test/myFunction.js`. Optionally tests can be created to specific folder using `--path` or `-p` switch, e.g. 

```
sls create function -f myFunction --handler functions/myFunction/index.handler --path tests
```

To create tests next to handler use `--path {function}`, in following example test file `myFunction.test.js` is created to `functions/myFunction/` directory.

```
sls create function -f myFunction --handler functions/myFunction/index.handler --path {function}
```

### Creating tests

Tests can also be added to existing handlers using

```
sls create test -f functionName
```

### Running tests

Tests can be run directly using Jest or using the "invoke test" command

```
sls invoke test [--stage stage] [--region region] [-f function]
```

If no function names are passed to "invoke test", all tests related to handler functions are run.

### Using own template for a test file

The templates to use for new function Files can be determined with the custom `testTemplate` configuration in `serverless.yml`

```
custom:
  serverless-jest-plugin:
    testTemplate: templates/myTest.js
```

Currently, there are three variables available for use in the template:

- functionName - name of the function
- functionPath - path to the function
- handlerName - the name of the handler function

If you'd like to get more information on the template engine, you check documentation of the [EJS project](http://ejs.co/).

## License
https://github.com/SC5/serverless-jest-plugin/blob/master/LICENSE