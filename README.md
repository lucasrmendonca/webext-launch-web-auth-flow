webext-launch-web-auth-flow
============

Polyfill `launchWebAuthFlow` with popups.

Installation
------------

### Via npm

```
npm install webext-launch-web-auth-flow
```

```js
const launchWebAuthFlow = require("webext-launch-web-auth-flow");

```

### Pre-built dist

You can find it under the `dist` folder, or [download from unpkg](https://unpkg.com/webext-launch-web-auth-flow/dist/).

Why
----

1. Builtin `launchWebAuthFlow` doesn't reuse the browser session. This library does.
2. Builtin `launchWebAuthFlow` doesn't allow custom redirect_uri. This library does.

Permission
-----------

To polyfill `launchWebAuthFlow`, this library uses following API/permissions:

1. `windows` and `tabs` - this library launches a window dialog (or tab in Firefox android) to login.
2. `webRequest` with `blocking` - this library cancels the request to `redirect_uri` so it won't leak the token/code to `redirect_uri` (or `redirect_uri` is unresolveable e.g. the URL from `identity.getRedirectURL`).
3. `webNavigation` - the login dialog is minimized unless there is no redirect. It checks the loading state using `webNavigation.onDOMContentLoaded`.

Compatibility
--------------

This library references the global `browser`. To make it work on Chrome, you need something like [webextension-polyfill](https://github.com/mozilla/webextension-polyfill)

API reference
-------------

This module exports a single function.

### webextLaunchWebAuthFlow

```js
launchWebAuthFlow({
  url: String,
  redirect_uri: String,
  interactive?: Boolean = false
}) => finalUrl: String
```

You have to pass `redirect_uri` explicitly.

See MDN for other arguments:
https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/identity/launchWebAuthFlow

Changelog
---------

* 0.1.0 (Next)

  - First release.
