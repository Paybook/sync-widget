### Events

---

<br />

Events are emitted by the widget under certain conditions in order to communicate the status of the synchronization of credentials to your application.

To handle this events, after creating your widget instance subscribe to those events using the syncWidget's `$on` method:

```javascript
...

syncWidget = new SyncWidget(params);

myCallbackForThisEvent = () => {
    /*
    * This is your registered callback that will be executed every
    * time this event is triggered by the Syncfy Widget
    */
    ....
}

syncWidget.$on('... some eventName ... ', myCallbackForThisEvent);
```

---

<br />

##### What values does each event emit?

Some events are `void` (meaning that they don't pass any data to the registered callback). However, if the event pass values to the registered callback, those values can be:

```json
// CredentialStatus value:
{
    "code": "Number"
}

// Credential value:
{
    "id_credential": "String",
    "username": "String",
    "is_new": "Number",
    "ws": "String",
    "status": "String",
    "twofa": "String"
}

// ApiError value:
{
    "longMessage": "String",
    "message": "String",
    "noInternet": "Boolean"
}

// JobError value:
{
    "code": "Number",
    "longMessage": "String",
    "message": "String"
}

// SocketError value:
{
    "longMessage": "String",
    "message": "String",
    "type": "error | timeout"
}
```

---

<br />

##### Event Types

The list of events available is described below:

`$on("opened", ... )`

```javascript
syncWidget.$on("opened", () => {
  // ... do something when the widget is opened ...
});
```

---

<br />

`$on("loaded", ... )`

```javascript
syncWidget.$on("loaded", () => {
  // ... do something when the widget is first loaded ...
});
```

---

<br />

`$on("dom-updated", ... )`

```javascript
syncWidget.$on("dom-updated", () => {
  // ... do something when the dom changes ...
});
```

---

<br />

`$on("images-loading", ... )`

```javascript
syncWidget.$on("images-loading", () => {
  // ... do something when more than 0 images are being loaded ...
});
```

---

<br />

`$on("images-loaded", ... )`

```javascript
syncWidget.$on("images-loaded", () => {
  // ... do something when all the images that were being loaded are loaded ...
});
```

---

<br />

`$on("closed", ... )`

```javascript
syncWidget.$on("closed", () => {
  // ... do something when the widget is closed ...
});
```

---

<br />

`$on("back", ... )`

```javascript
syncWidget.$on("back", () => {
  // ... do something when a back button is clicked ...
});
```

---

<br />

`$on("updated", ... )`

```javascript
syncWidget.$on("updated", (status: CredentialStatus) => {
  /*
    * In particular, this event is triggered after the Syncfy 
    * API responds that it has received the credential values, 
    * *and the synchronization process is about to start
    * 
    ... do something when a new synchronization status is reached ...
    */
});
```

---

<br />

`$on("submitted", ... )`

```javascript
syncWidget.$on("submitted", () => {
  // ... do something when a form is submitted ...
});
```

---

<br />

`$on("status", ... )`

```javascript
syncWidget.$on("status", (status: CredentialStatus) => {
  /*
    * In particular, this event is triggered while the synchronization status 
    * is running and after each change in the synchronization status this
    * event is triggered with the current's status data

    ... do something when a new synchronization status is reached ...
    */
});
```

For details on which are the statuses and more details on this consult the Syncfy API docs.

---

<br />

`$on("success", ... )`

```javascript
syncWidget.$on("success", (credential: Credential) => {
  // ... do something when the synchronization of a credential is finished successfully
});
```

---

<br />

`$on("error", ... )`

```javascript
syncWidget.$on("error", (credential: Credential, jobError: JobError) => {
  // ... do something when there is some error in the synchronization of credentials  ...
  // ... jobError is not send if the socket timeouts, for socket errors use socket-error event ...
});
```

For details on which errors might happend and how to handle them, consult the Syncfy API docs.

---

<br />

`$on("401", ... )`

Event 401 is triggered when the user session is unauthorized.

```javascript
syncWidget.$on("401", () => {
  // ... do something when user session is unauthorized.
  // i.e. refresh user session.
});
```

---

<br />

`$on("api-error", ... )`

Event api-error is triggered when making call to Syncfy API returns an error status code. For a list of `statusCode` meaning check **Codes** section, the code could also be "credential_not_found" or "site_not_found".

```javascript
syncWidget.$on("api-error", (statusCode, apiError: ApiError) => {
  // ... do something on api error.
  // i.e. refresh user session.
});
```

<br />

`$on("socket-error", ... )`

Event socket-error is triggered when the socket timeouts or the connection closed unexpectedly.

```javascript
syncWidget.$on("socket-error", (socketError: SocketError) => {
  // ... do something on socket error.
});
```
