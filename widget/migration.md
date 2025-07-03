# Migration Guide: Syncfy Widget v2 → Syncfy Widget v3

This guide will help you migrate your integration from the **Syncfy Widget v2** to the **Syncfy Widget v3**.  
It highlights the main differences, new features, and breaking changes between the two versions.

---

## Table of Contents

- Overview
- Naming
- Parameter & Config Changes
- Rendering
- Configuration Differences Table
- Method Differences Table
- Event Changes
- Sample Migration
- Summary Table

---

## Overview

- **SyncWidget** is now called **SyncfyWidget**.
- The new version (SyncfyWidget) is a superset of the previous one, with more configuration options, more events, and improved documentation.
- Some defaults and method/event names have changed.
- The new version is still framework-agnostic and easy to integrate.

---

## Naming

- Update all references from `SyncWidget` to `SyncfyWidget`.
- NPM package and CDN URL are different, see overview to implement new changes.

---

## Parameter & Config Changes

### 1. **Initialization**

**Old:**

```js
const params = {
  token,
  element: "#widget",
  config: { ... }
};
syncWidget = new SyncWidget(params);
```

**New:**

```js
const params = {
  token,
  element: "#widget",
  config: { ... }
};
syncfyWidget = new SyncfyWidget(params);
```

## Rendering

In the old Widget, the provided element was replaced by the Widget. In the new Widget, the Widget is appended inside the provided element.

---

## Configuration Differences Table

| **Attribute**                         | **Sync Widget (Old)** | **Syncfy Widget (New)** | **Notes/Action**                                                                   |
| ------------------------------------- | --------------------- | ----------------------- | ---------------------------------------------------------------------------------- |
| `client`                              | ❌                    | ✅                      | New: Add for branding (logo, name).                                                |
| `client.logo`                         | ❌                    | ✅                      | New: Logo URL for branding.                                                        |
| `client.name`                         | ❌                    | ✅                      | New: Client name for branding.                                                     |
| `entrypoint.updateCredential`         | ❌                    | ✅                      | New: Open widget in UpdateCase for a credential, only non-identifier fields shown. |
| `locale` default                      | `"es"`                | `"en"`                  | Default changed; set explicitly if you want Spanish.                               |
| `navigation.displayCredentialInModal` | ❌                    | ✅                      | New: Show credential process in toast or modal.                                    |
| `navigation.displayPrivacyScreen`     | ❌                    | ✅                      | New: Show privacy policy screen before syncing.                                    |
| `navigation.hideAsideMenu`            | ✅                    | ❌                      | In the new widget, the menu doesn't exist.                                         |
| `navigation.quickAnswer`              | `quickanswer`         | `quickAnswer`           | Typo fixed: use `quickAnswer`.                                                     |
| `navigation.toastPosition`            | Fewer options         | More options            | Now supports `top-center` and `bottom-center`.                                     |

---

## Method Differences Table

| **Method**                                    | **Sync Widget (Old)**         | **Syncfy Widget (New)**                          | **Notes/Action**                                                       |
| --------------------------------------------- | ----------------------------- | ------------------------------------------------ | ---------------------------------------------------------------------- |
| `getLastRid()`                                | ❌                            | `syncfyWidget.getLastRid()`                      | New: Returns last rid from API calls.                                  |
| `on(eventName, callback)`                     | `syncWidget.$on("event", cb)` | `syncfyWidget.on("event", cb)`                   | Changed: Use `.on` instead of `.$on`.                                  |
| `setEntrypointUpdateCredential(idCredential)` | ❌                            | `syncfyWidget.setEntrypointUpdateCredential(id)` | New: Open UpdateCase for credential, only non-identifier fields shown. |

---

## Event Changes

- New events have been introduced, and some old events have been removed or renamed.

| **Event Name**                 | **Old Version** | **New Version** | **Notes**                                        |
| ------------------------------ | :-------------: | :-------------: | ------------------------------------------------ |
| `"401"`                        |       ❌        |       ✅        | Triggered when an API call is unauthorized.      |
| `"api-error"`                  |       ❌        |       ✅        | Triggered when an API call fails.                |
| `"loaded"`                     |       ❌        |       ✅        | Triggered when the first information is loaded.  |
| `"organization-selected"`      |       ❌        |       ✅        | Triggered when an organization site is selected. |
| `"organization-site-selected"` |       ❌        |       ✅        | Triggered when a site is selected.               |
| `"privacy-accepted"`           |       ❌        |       ✅        | Triggered when privacy policy is accepted.       |
| `"socket-error"`               |       ❌        |       ✅        | Triggered after the websocket fails.             |

**Migration:**

- Update your event handling code to accommodate the new event names and structures.

---

## Sample Migration

**Old Code:**

```js
const params = {
  token: "your-token",
  element: "#widget",
  config: {
    // old config options
  },
};
syncWidget = new SyncWidget(params);

syncWidget.$on("opened", () => {
  console.log("Widget opened");
});

syncWidget.open();
```

**New Code:**

```js
const params = {
  token: "your-token",
  element: "#widget",
  config: {
    client: {
      name: "Chipi",
      logo: "https://chipi.com/logo.svg",
    },
    // new config options
  },
};
syncfyWidget = new SyncfyWidget(params);

syncfyWidget.on("opened", () => {
  console.log("Syncfy Widget opened");
});

syncfyWidget.open();
```

---

## Summary Table

| Feature/Aspect        | Old Version (Sync Widget) | New Version (Syncfy Widget)    |
| --------------------- | ------------------------- | ------------------------------ |
| Name                  | SyncWidget                | SyncfyWidget                   |
| Initialization Method | `new SyncWidget()`        | `new SyncfyWidget()`           |
| Rendering             | Replaces element.         | Appended inside element.       |
| Event Subscription    | `.$on()`                  | `.on()`                        |
| Branding              | Not available.            | `client` object.               |
| Configuration Options | Fewer options.            | More options.                  |
| Method Names          | Some missing.             | More methods, see table above. |
| Events                | Fewer.                    | More events, see table above.  |

---
