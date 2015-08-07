env2
===

[![Build Status](https://travis-ci.org/dwyl/env.svg)](https://travis-ci.org/dwyl/env)
[![Test Coverage](https://codeclimate.com/github/dwyl/env/badges/coverage.svg)](https://codeclimate.com/github/dwyl/env/coverage)
[![Code Climate](https://codeclimate.com/github/dwyl/env/badges/gpa.svg)](https://codeclimate.com/github/dwyl/env)
[![Dependency Status](https://david-dm.org/dwyl/env.svg)](https://david-dm.org/dwyl/env)
[![devDependency Status](https://david-dm.org/dwyl/env/dev-status.svg)](https://david-dm.org/dwyl/env#info=devDependencies)
[![npm](https://img.shields.io/npm/v/env2.svg)](https://www.npmjs.com/package/env2)

## Why?

Quoting [The Twelve Factor App](http://12factor.net/config) section 3:

> "**Store config in the environment**"

"*An app’s config is everything that is likely to vary between deploys
(staging, production, developer environments, etc)*".

This means we need a simple/reliable way of managing **environment variables**;
**env2** *is* ***the way***.

## What?

env2 allows you to store your environment variables in an `env.json` file
which gets loaded when your app starts.

All the entries in the `env.json` file are available as keys in
the `process.env` object.

## How?

First create an `env.json` file in your repo:

```js
{
  "DB_HOST": "127.0.0.1",
  "DB_PORT": 9200,
  "DB_USER": "anon",
  "DB_PASS": "password"
}
```
if you don't want your `env.json` to be in your version control
(i.e. _visible on GitHub_) simply *add* the filename to your `.gitignore` file:

```sh
echo 'env.json' >> .gitignore
```

### Install from NPM

Next install `env2` from npm and save it to your `package.json` file:

```sh
npm install env2 --save
```

### Use in your Code

Then in your script/module:

```javascript
var env = require('env2')('./path-to-your/env.json')

// your app goes here
console.log(process.env.DB_HOST); // "127.0.0.1"
```

Env is synchronous; it loads all your configuration variables into the
`process.env` object *before* app/script execution.

<br />

## Do you want to Define Priority for Variables?

Do you want the ability to *specify* the priority which
environment variables take precendence?
e.g: if you supply a command-line argument when running your script/app:
```sh
evn=PROD API_KEY=token.dwyl.yolo node myapp.js
```
We have an open discussion around this: https://github.com/dwyl/env2/issues/1

At present, any environment variable defined in the environment where
your app is running (or via command-line arguments) will take
precendence over the same key in your `env.json` file ... if you prefer
to have the option to *specify* the priority, please add a comment to the isssue:
https://github.com/dwyl/env2/issues/1

## Name ?

**Q**: Why is it called "env2"?  
**A**: as the digit in the name suggests, there was/is an "env" (version 1):
https://www.npmjs.com/package/env written by [@dshaw](https://github.com/dshaw)
sadly, it was never finished and has not been updated in 4 years ...
We asked Dan if he would accept a Pull Request updating the package:
https://github.com/dshaw/env/issues/6 and he said he *would* accept it ...
But after investing the time and submitting the pull request:
https://github.com/dshaw/env/pull/8 which updated the package to the latest
version of Node/io.js and had tests & 100% coverage, the PR got ignored.
see: https://twitter.com/dshaw/status/628237150253772801
Not that we're "_impatient_" but we need to move on with our code/lives.
If the PR to env ever gets merged, we *could* use that instead,
but actually **env2** is ***much simpler*** and servers our needs better,
so we are probably going to stick with the "***New and Improved***" Version.
