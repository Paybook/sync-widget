##### How to install it?

There are two ways to install the Syncfy Authentication Widget

_[1] Using Node Package Manager:_

The first step is to install [@syncfy/authentication-widget](https://www.npmjs.com/package/@syncfy/authentication-widget) with NPM:

```bash
npm install --save @syncfy/authentication-widget
```

And then import the widget styles to your app:

```css
@import "@syncfy/authentication-widget/dist/syncfy-authentication-widget.css";
```

And finally get access to the `SyncfyWidget` class by importing it:

```javascript
import SyncfyWidget from "@syncfy/authentication-widget";
```

_[2] Using CDN:_

To install it via CDN import the following files in your _index.html_ file:

Add this line in the `<head>` element:

```html
<link
  rel="stylesheet"
  href="https://syncfy.com/widget/v3/syncfy-authentication-widget.css"
/>
```

And add this line in the `<body>` element:

```html
<script
  type="text/javascript"
  src="https://syncfy.com/widget/v3/syncfy-authentication-widget.js"
></script>
```

This will expose the `SyncfyWidget` class in the global window object.

---

<br />

##### Where can I use it?

First of all, since the widget is coded in vanilla JavaScript, you can use it in any web application, no matter what framework you use (React, Vue, Angular, jQuery, etc).

To use the widget, follow this checklist:

- Sign up for your Syncfy API account to get your API keys.
- Create a session token. For this, refer to the [Syncfy API documentation](<https://syncfy.com/w/en/sync/public/app/(section:docs/mx/sync/api/sessions)>) on how to create a session and obtain a token (you will need your API keys).
- In your frontend application, import the Syncfy Widget files (.js and .css) or install the widget using NPM.
- Configure the widget as desired and instantiate it using the token you already have.
- Start adding or updating credentials—and that's it!

---

<br />

##### What can I do with the Syncfy Widget?

You can use the _Syncfy Widget_ for the following use cases:

- **To create a credential:** Use the Syncfy Widget to create a new credential, that is, to connect to a bank or site for the first time.
- **To update an existing credential:** Use the Syncfy Widget to update an existing credential, such as updating the username, password, etc., of a credential you added in the past.
- **To re-sync credentials:** Keep a credential up to date by forcing the synchronization process whenever your end-users desire, or periodically run the synchronization for credentials that require a token (two-factor authentication).

---

<br />

##### Where can I learn how to implement it and customize it?

There is plenty of documentation and resources that will help you implement the Syncfy Widget, namely:

- Widget Configuration: how to configure the widget.
- Widget Methods: the methods you can use to set up and manipulate the widget.
- Widget Events: how to catch events and handle communication between the widget and your application.
- Widget Use Cases: how to set up the widget for different cases.
- Widget Examples: see some examples.
