# ember-cli-custom-assertions #

## About ##

Add custom assertions to your Ember test suite.

## Installing ##

`ember install ember-cli-custom-assertions`

## Looking for help? ##

If it is a bug [please open an issue on GitHub](https://github.com/dockyard/ember-cli-custom-assertions/issues).

## Usage ##

Add new assertions to `test/assertions`. Then use on the `assert` object in your test suite.

For example:

```javascript
// tests/assertions/contains.js

export default function(context, element, text, message) {
  var matches = context.$(element).text().match(new RegExp(text));
  message = message || `${element} should contain "${text}"`;

  this.push(!!matches, matches, text, message);
}

// tests/acceptance/foo-test.js
test('foo is bar', function(assert) {
  visit('/');

  andThen(function() {
    assert.contains('Foo Bar');
  });
});
```

### Assertion

A `context` is always injected as the first argument. You don't need to
pass a context when calling the assertion, only when injecting the insertions into your app.

```js
// good
assert.contains('.foo', 'Foo bar');

// bad
assert.contains(app, '.foo', 'Foo bar');
```

### Setup

You must inject the assertions and pass the context along.

For example, with acceptance tests you can inject in `beforeEach` and
cleanup in `afterEach`:

```javascript
// ...
import { assertionInjector, assertionCleanup } from '../assertions'; 

module('Acceptance | foo', {
  beforeEach: function() {
    var application = startApp();
    assertionInjector(application);
  },

  afterEach: function() {
    Ember.run(application, 'destroy');
    applicationCleanup(application);
  }
});
```

## Authors ##

* [Brian Cardarella](http://twitter.com/bcardarella)

[We are very thankful for the many contributors](https://github.com/dockyard/ember-cli-custom-assertions/graphs/contributors)

## Versioning ##

This library follows [Semantic Versioning](http://semver.org)

## Want to help? ##

Please do! We are always looking to improve this library. Please see our
[Contribution Guidelines](https://github.com/dockyard/ember-cli-custom-assertions/blob/master/CONTRIBUTING.md)
on how to properly submit issues and pull requests.

## Legal ##

[DockYard](http://dockyard.com), Inc &copy; 2015

[@dockyard](http://twitter.com/dockyard)

[Licensed under the MIT license](http://www.opensource.org/licenses/mit-license.php)
