# Syncfy Widget Methods

---

The _Syncfy Widget_ instance exposes several methods to configure and control the widget. Most methods update the widget's configuration or state, but do not automatically re-render the UI. To see changes reflected, call `syncfyWidget.open()` after updating the configuration (unless otherwise noted).

Below are the main methods available on a Syncfy Widget instance:

---

## open()

```javascript
// Opens the Syncfy Widget modal or UI.
syncfyWidget.open();
```

Use this method to open the widget. Call this after updating configuration to re-render the UI.

---

<br />

## close()

```javascript
// Closes the Syncfy Widget modal or UI.
syncfyWidget.close();
```

Use this method to close the widget.

---

<br />

## setConfig(widgetConfig: WidgetConfig)

```javascript
// Fully replace the current widget configuration.
syncfyWidget.setConfig({
  // ... a valid WidgetConfig object ...
});
```

This method completely replaces the current configuration. Call `open()` to apply changes.

---

<br />

## upsertConfig(widgetConfig: WidgetConfig)

```javascript
// Patch or upsert the current configuration.
syncfyWidget.upsertConfig({
  // ... a partial WidgetConfig object ...
});
```

This method merges the given config with the current configuration. Call `open()` to apply changes.

---

<br />

## setToken(token: String)

```javascript
// Set or replace the authentication token.
syncfyWidget.setToken("...a valid Syncfy API token...");
```

Use this method to update the token for authentication. Call `open()` if you want to refresh the UI with the new token.

---

<br />

## setEntrypointCredential(idCredential: String)

```javascript
// Open the widget for the given credential (re-synchronization case).
syncfyWidget.setEntrypointCredential("...credential-id...");
```

This method triggers the synchronization process for the specified credential. The status toast will open immediately. You do not need to call `open()` after this method.

---

<br />

## setEntrypointSite(idSite: String)

```javascript
// Set the widget entrypoint to a specific site (for updating credentials).
syncfyWidget.setEntrypointSite("...site-id...");
```

When set, the widget will start in the given site, ready to update credentials (username, password, etc.). If the user enters credentials for an existing account, the Syncfy API will update the credential. Call `open()` to show the UI for the new entrypoint.

---

## setEntrypointUpdateCredential(idCredential: String)

```javascript
// Open the widget in UpdateCase for the given credential (only non-identifier fields).
syncfyWidget.setEntrypointUpdateCredential("...credential-id...");
```

This method opens the widget in UpdateCase for the specified credential, showing only non-identifier fields. You do not need to call `open()` after this method.

---

## getLastRid()

```javascript
// Get the last request ID (rid) from API calls.
const rid = syncfyWidget.getLastRid();
```

Returns the last request ID used in API calls. Useful for debugging or tracking requests.

---

## on(eventName: String, callback: Function)

```javascript
// Listen to Syncfy Widget events.
syncfyWidget.on("opened", () => {
  // ...do something when the widget is opened...
});
```

Use this method to subscribe to widget events. Common event names include: `"401"`, `"error"`, `"success"`, `"status"`, `"updated"`, `"submitted"`, `"back"`, `"opened"`, and `"closed"`. See the **Events** section for more details.
