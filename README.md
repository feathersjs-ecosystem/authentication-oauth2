# @feathersjs/authentication-oauth2

> __Important:__ The code for this module has been moved into the main Feathers repository at [feathersjs/feathers](https://github.com/feathersjs/feathers) ([package direct link](https://github.com/feathersjs/feathers/tree/master/packages/authentication-oauth2)). Please open issues and pull requests there. No changes in your existing Feathers applications are necessary.

[![Build Status](https://travis-ci.org/feathersjs/authentication-oauth2.png?branch=master)](https://travis-ci.org/feathersjs/authentication-oauth2)

An OAuth2 authentication strategy for feathers-authentication using Passport

## Installation

```
npm install @feathersjs/authentication-oauth2 --save
```

**Note:** This is only compatibile with `feathers-authentication@1.x` and above.

## Quick example

```js
const feathers = require('@feathersjs/feathers');
const authentication = require('feathers-authentication');
const jwt = require('feathers-authentication-jwt');
const oauth2 = require('@feathersjs/authentication-oauth2');
const FacebookStrategy = require('passport-facebook').Strategy;
const app = feathers();

// Setup authentication
app.configure(authentication(settings));
app.configure(jwt());
app.configure(oauth2({
  name: 'facebook',
  Strategy: FacebookStrategy,
  clientID: '<your client id>',
  clientSecret: '<your client secret>',
  scope: ['public_profile', 'email']
}));

// Setup a hook to only allow valid JWTs to authenticate
// and get new JWT access tokens
app.service('authentication').hooks({
  before: {
    create: [
      authentication.hooks.authenticate(['jwt'])
    ]
  }
});
```

## Documentation

Please refer to the [@feathersjs/authentication-oauth2 API documentation](https://docs.feathersjs.com/api/authentication/oauth2.html) for more details.

## License

Copyright (c) 2018

Licensed under the [MIT license](LICENSE).
