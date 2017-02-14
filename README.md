Raven
============

Raven/[Sentry](https://www.getsentry.com) integration for Meteor. Includes [Raven.js](https://github.com/getsentry/raven-js) for frontend logging and [raven-node](https://github.com/mattrobenolt/raven-node) for backend logging.

Provides consolidated error logging to Sentry via Raven from both the client and the server.

This package is MIT Licensed. Do whatever you like with it but any responsibility for doing so is your own. All rights to raven are with the original authors.

Main differences to deepwell:raven
============

- This package doesn't embed the browser code. Instead, it pulls it from npm
- Raven libs updated to most recent versions.

Usage
============
Configure your client and server DSN keys and log an error message. For the
client entry, don't include your private key. For the server entry, **include your private key.**

```javascript
RavenLogger.initialize({
  client: 'https://public_key@app.getsentry.com/app_id',            // Do not include your private key here
  server: 'https://public_key:private_key@app.getsentry.com/app_id' // *DO* include your private key here
});
RavenLogger.log('Testing error message');
```

Optionally you can pass a tag:

```javascript
RavenLogger.log('Testing error message', { component: 'system' });
```

To set tags on the whole context, use `RavenLogger.setTagsContext`:

```javascript
RavenLogger.setTagsContext({ component: 'system' });
```

If you are using the Meteor Accounts package, you can enable user tracking on errors:

```javascript
RavenLogger.initialize({
  client: 'your client DSN here',
  server: 'your server DSN here'
}, {
  trackUser: true
});
```

To catch uncaught exceptions on the server, set patchGlobal to true or a function:

```javascript
RavenLogger.initialize({
  client: 'your client DSN here',
  server: 'your server DSN here'
});
```

Raven also works very well with saving full error and exception stack traces. Simply pass an Error or a Meteor.Error object to the log method to keep the stack trace.

```javascript
RavenLogger.log(new Meteor.Error(422, 'Failed to save object to database'));
```
