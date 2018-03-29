# ember-intercom-io

[![Greenkeeper badge](https://badges.greenkeeper.io/mike-north/ember-intercom-io.svg)](https://greenkeeper.io/)

[![Build Status](https://travis-ci.org/mike-north/ember-intercom-io.svg?branch=master)](https://travis-ci.org/mike-north/ember-intercom-io)
[![Code Climate](https://codeclimate.com/github/mike-north/ember-intercom-io/badges/gpa.svg)](https://codeclimate.com/github/mike-north/ember-intercom-io)
[![Dependency Status](https://david-dm.org/mike-north/ember-intercom-io.svg)](https://david-dm.org/mike-north/ember-intercom-io)
[![devDependency Status](https://david-dm.org/mike-north/ember-intercom-io/dev-status.svg)](https://david-dm.org/mike-north/ember-intercom-io#info=devDependencies)
[![Ember Observer Score](http://emberobserver.com/badges/ember-intercom-io.svg)](http://emberobserver.com/addons/ember-intercom-io)

[Intercom.io](http://intercom.io) for Ember.js apps.

## Setup

**Install this addon with ember-cli** `ember install ember-intercom-io`

**Add the `{{intercom-io}}` component to one of your templates`**
The chat widget will appear whenever this component has been rendered, and should disappear whenever it's destroyed.

### Configuration

**In your `config/environment.js` file, you must provide your `appId`**

```js

module.exports = function(environment) {
  ...
  intercom: {
    appId: null, // <-- REPLACE WITH YOUR INTERCOM.IO app_id
    enabled: true, // <-- Setting to false in your testing environment prevents unneccessary network requests (true by default)
  },
  ...
};

```


#### Users vs Leads

In the intercom.io world, a lead is a visitor to your site or app, without an email or name associated with them. A user has a name and email, and is a good construct for tracking the history of all interactions w/ a single person.

You can make `ember-intercom-io` aware of a "user" context (shifting into "users" mode instead of "leads" mode) by adding an object to the `intercom` service (i.e., your user authentication service).

**app/services/authentication.js**
```js
import Ember from 'ember';

const { inject } = Ember;

export default Ember.Service.extend({
  intercom: inject.service(), // the intercom service
  didLogin(user) {
    ...
    this.get('intercom').set('user.name', 'Joe Username');
    this.get('intercom').set('user.email', 'joe@example.com');
    this.get('intercom').set('user.createdAt', 1447135065173);
  }
});

```

## API

The `intercom` service exposes several public API methods that match Intercom.com's
existing Javascript API. For full details on the client API, [read the Intercom docs.](https://developers.intercom.com/v2.0/docs/intercom-javascript#section-intercomonhide)

### Properties

|    Name      |      Type         |
------------------------------------
| autoUpdate   | Boolean           |
| hideDefaultLauncher | Boolean    |
| isOpen       | Boolean           |
| isBooted     | Boolean           |
| unreadCount  | Integer           |
| user         | Object            |

### Methods

The following intercom methods are implemented. See `services/intercom.js` for full
details.

`boot()`

`update()`

`shutdown()`

`hide()`

`show()`

`showMessages()`

`showNewMessage()`

`trackEvent()`

`getVisitorId()` Returns the current id of the logged in user.

### Events

Subscribe to events in your app with event listeners:

```js
//fancy-component.js

...

intercom: Ember.inject.service(),
newMessageAlert: Ember.on('intercom.unreadCountChange', function() {
    alert('Unread Count Changed!');
}),

...

```

**Available Events**

(Read the Intercom documentation for full details)[https://developers.intercom.com/v2.0/docs/intercom-javascript#section-intercomonhide]

| Ember Event | Intercom Event |
--------------------------------
| hide        | `onHide`       |
| show        | `onShow`       |
| unreadCountChange | `onUnreadCountChange` |


## Installation

* `git clone` this repository
* `npm install`
* `bower install`

### Linting

* `npm run lint:js`
* `npm run lint:js -- --fix`

### Running tests

* `ember test` – Runs the test suite on the current Ember version
* `ember test --server` – Runs the test suite in "watch mode"
* `npm test` – Runs `ember try:each` to test your addon against multiple Ember versions

### Running the dummy application

* `ember serve`
* Visit the dummy application at [http://localhost:4200](http://localhost:4200).

For more information on using ember-cli, visit [http://www.ember-cli.com/](http://www.ember-cli.com/).

Copyright (c) 2015 Levanto Financial, 2016-18 [Mike Works](https://mike.works), Inc.
