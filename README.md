# passport-oauth1

[![Build](https://img.shields.io/travis/jaredhanson/passport-oauth1.svg)](https://travis-ci.org/jaredhanson/passport-oauth1)
[![Coverage](https://img.shields.io/coveralls/jaredhanson/passport-oauth1.svg)](https://coveralls.io/r/jaredhanson/passport-oauth1)
[![Quality](https://img.shields.io/codeclimate/github/jaredhanson/passport-oauth1.svg?label=quality)](https://codeclimate.com/github/jaredhanson/passport-oauth1)
[![Dependencies](https://img.shields.io/david/jaredhanson/passport-oauth1.svg)](https://david-dm.org/jaredhanson/passport-oauth1)


General-purpose OAuth 1.0 authentication strategy for [Passport](http://passportjs.org/).

This module lets you authenticate using OAuth in your Node.js applications.
By plugging into Passport, OAuth authentication can be easily and unobtrusively
integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

Note that this strategy provides generic OAuth support.  In many cases, a
provider-specific strategy can be used instead, which cuts down on unnecessary
configuration, and accommodates any provider-specific quirks.  See the
[list](https://github.com/jaredhanson/passport/wiki/Strategies) for supported
providers.

Developers who need to implement authentication against an OAuth provider that
is not already supported are encouraged to sub-class this strategy.  If you
choose to open source the new provider-specific strategy, please add it to the
list so other people can find it.

## Install

    $ npm install passport-oauth1

## Usage

#### Configure Strategy

The OAuth authentication strategy authenticates users using a third-party
account and OAuth tokens.  The provider's OAuth endpoints, as well as the
consumer key and secret, are specified as options.  The strategy requires a
`verify` callback, which receives a token and profile, and calls `cb`
providing a user.

    passport.use(new OAuth1Strategy({
        requestTokenURL: 'https://www.example.com/oauth/request_token',
        accessTokenURL: 'https://www.example.com/oauth/access_token',
        userAuthorizationURL: 'https://www.example.com/oauth/authorize',
        consumerKey: EXAMPLE_CONSUMER_KEY,
        consumerSecret: EXAMPLE_CONSUMER_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/example/callback",
        signatureMethod: "RSA-SHA1"
      },
      function(token, tokenSecret, profile, cb) {
        User.findOrCreate({ exampleId: profile.id }, function (err, user) {
          return cb(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'oauth'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/example',
      passport.authenticate('oauth'));
    
    app.get('/auth/example/callback', 
      passport.authenticate('oauth', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Related Modules

- [passport-oauth2](https://github.com/jaredhanson/passport-oauth2) — OAuth 2.0 authentication strategy
- [passport-http-oauth](https://github.com/jaredhanson/passport-http-oauth) — OAuth authentication strategy for APIs
- [oauthorize](https://github.com/jaredhanson/oauthorize) — OAuth service provider toolkit

## Contributing

#### Tests

The test suite is located in the `test/` directory.  All new features are
expected to have corresponding test cases.  Ensure that the complete test suite
passes by executing:

```bash
$ make test
```

#### Coverage

All new feature development is expected to have test coverage.  Patches that
increse test coverage are happily accepted.  Coverage reports can be viewed by
executing:

```bash
$ make test-cov
$ make view-cov
```

## Support

#### Funding

This software is provided to you as open source, free of charge.  The time and
effort to develop and maintain this project is dedicated by [@jaredhanson](https://github.com/jaredhanson).
If you (or your employer) benefit from this project, please consider a financial
contribution.  Your contribution helps continue the efforts that produce this
and other open source software.

Funds are accepted via [PayPal](https://paypal.me/jaredhanson), [Venmo](https://venmo.com/jaredhanson),
and [other](http://jaredhanson.net/pay) methods.  Any amount is appreciated.

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2011-2016 Jared Hanson <[http://jaredhanson.net/](http://jaredhanson.net/)>

<a target='_blank' rel='nofollow' href='https://app.codesponsor.io/link/vK9dyjRnnWsMzzJTQ57fRJpH/jaredhanson/passport-oauth1'>  <img alt='Sponsor' width='888' height='68' src='https://app.codesponsor.io/embed/vK9dyjRnnWsMzzJTQ57fRJpH/jaredhanson/passport-oauth1.svg' /></a>
