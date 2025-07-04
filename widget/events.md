# Syncfy Widget Events

---

The Syncfy Widget emits events to communicate status, progress, and errors to your application. You can subscribe to these events using the `on` method of your widget instance.

## How to Listen to Events

```javascript
const syncfyWidget = new SyncfyWidget(params);

function myCallbackForThisEvent(data) {
  // This function will be called whenever the event is triggered.
}

syncfyWidget.on("event-name", myCallbackForThisEvent);
```

> Replace `'event-name'` with the name of the event you want to listen for. The callback receives event-specific data (see below).

---

<br />

## Event Payloads

Some events do not pass any data to the callback (void), while others provide useful information. Here are the main payload types:

- **CredentialStatus**
  ```json
  { "code": Number }
  ```
- **Credential**
  ```json
  { "id_credential": String, "username": String, "is_new": Number, "ws": String, "status": String, "twofa": String }
  ```
- **ApiError**
  ```json
  { "longMessage": String, "message": String, "noInternet": Boolean }
  ```
- **JobError**
  ```json
  { "code": Number, "longMessage": String, "message": String }
  ```
- **SocketError**
  ```json
  { "longMessage": String, "message": String, "type": "error" | "timeout" }
  ```

---

<br />

## Event List

Below are the main events you can listen for. All events use the `on` method (not `$on`).

---

### "401"

Triggered when the user session is unauthorized.
**Data:** none

```javascript
syncfyWidget.on("401", () => {
  // ... do something when user session is unauthorized ...
});
```

---

### "api-error"

Triggered when a Syncfy API call returns an error status code.
**Data:** `(statusCode: Number | String, apiError: ApiError)`

```javascript
syncfyWidget.on("api-error", (statusCode, apiError) => {
  // ... do something on API error ...
});
```

---

### "back"

Triggered when a back button is clicked.
**Data:** none

```javascript
syncfyWidget.on("back", () => {
  // ... do something when a back button is clicked ...
});
```

---

### "back-up-site"

Triggered when the user navigates back up a site.
**Data:** none

```javascript
syncfyWidget.on("back-up-site", () => {
  // ... do something when navigating back up a site ...
});
```

---

### "back-up-site-submitted"

Triggered when the back-up-site form is submitted.
**Data:** none

```javascript
syncfyWidget.on("back-up-site-submitted", () => {
  // ... do something when back-up-site is submitted ...
});
```

---

### "closed"

Triggered when the widget is closed.
**Data:** none

```javascript
syncfyWidget.on("closed", () => {
  // ... do something when the widget is closed ...
});
```

---

### "dom-updated"

Triggered when the DOM changes.
**Data:** none

```javascript
syncfyWidget.on("dom-updated", () => {
  // ... do something when the DOM changes ...
});
```

---

### "error"

Triggered when there is an error in the synchronization of credentials.
**Data:** `(credential: Credential, jobError: JobError)`

```javascript
syncfyWidget.on("error", (credential, jobError) => {
  // ... do something when there is a synchronization error ...
});
```

---

### "images-loaded"

Triggered when all images have finished loading.
**Data:** none

```javascript
syncfyWidget.on("images-loaded", () => {
  // ... do something when all images are loaded ...
});
```

---

### "images-loading"

Triggered when images are being loaded.
**Data:** none

```javascript
syncfyWidget.on("images-loading", () => {
  // ... do something when images are loading ...
});
```

---

### "loaded"

Triggered when the widget is first loaded.
**Data:** none

```javascript
syncfyWidget.on("loaded", () => {
  // ... do something when the widget is first loaded ...
});
```

---

### "opened"

Triggered when the widget is opened.
**Data:** none

```javascript
syncfyWidget.on("opened", () => {
  // ... do something when the widget is opened ...
});
```

---

### "organization-selected"

Triggered when an organization site is selected.
**Data:** `{ id_organization: String, ... }` (object with organization info)

```javascript
syncfyWidget.on("organization-selected", (data) => {
  // ... do something when an organization site is selected ...
});
```

---

### "organization-site-selected"

Triggered when a site is selected within an organization.
**Data:** `{ id_site: String, ... }` (object with site info)

```javascript
syncfyWidget.on("organization-site-selected", (data) => {
  // ... do something when a site is selected ...
});
```

---

### "privacy-accepted"

Triggered when the privacy policy is accepted by the user.
**Data:** none

```javascript
syncfyWidget.on("privacy-accepted", () => {
  // ... do something when privacy policy is accepted ...
});
```

---

### "socket-error"

Triggered when the socket times out or the connection closes unexpectedly.
**Data:** `(socketError: SocketError)`

```javascript
syncfyWidget.on("socket-error", (socketError) => {
  // ... do something on socket error ...
});
```

---

### "status"

Triggered while the synchronization status is running and after each change in status.
**Data:** `(status: CredentialStatus)`

```javascript
syncfyWidget.on("status", (status) => {
  // ... do something when a new synchronization status is reached ...
});
```

---

### "submitted"

Triggered when a form is submitted.
**Data:** none

```javascript
syncfyWidget.on("submitted", () => {
  // ... do something when a form is submitted ...
});
```

---

### "success"

Triggered when the synchronization of a credential finishes successfully.
**Data:** `(credential: Credential)`

```javascript
syncfyWidget.on("success", (credential) => {
  // ... do something when synchronization is successful ...
});
```

---

### "updated"

Triggered after the Syncfy API receives credential values and the synchronization process is about to start.
**Data:** `(status: CredentialStatus)`

```javascript
syncfyWidget.on("updated", (status) => {
  // ... do something when a new synchronization status is reached ...
});
```
