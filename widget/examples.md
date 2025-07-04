## Examples

---

<br />

This is the simplest code snippet to get started with the Syncfy Widget. You can further configure the widget as needed:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <link
      rel="stylesheet"
      href="https://www.syncfy.com/widget/v3/syncfy-authentication-widget.css"
    />
    <title>Syncfy Widget</title>
  </head>
  <body>
    <div id="widget"></div>
    <script
      type="text/javascript"
      src="https://www.syncfy.com/widget/v3/syncfy-authentication-widget.js"
    ></script>
    <script>
      var params = {
        // Required: set up the token
        token: "<TOKEN_HERE>",
        // Optional: specify the element or selector where the widget will be rendered
        element: "#widget",
        // Optional: widget configuration object
        config: {
          // See below for configuration options
        },
      };
      var syncfyWidget = new SyncfyWidget(params);
      syncfyWidget.open();
    </script>
  </body>
</html>
```

<br />

Below is the default configuration used by the widget if you do not provide a `config` object (apart from the required parameters):

```json
{
  "locale": "es", // Default language is Spanish
  "entrypoint": {
    "country": "MX" // Default country is Mexico
  },
  "navigation": {
    "disableFormAutocomplete": false,
    "displayBusinessSites": true,
    "displayCredentialInModal": false,
    "displayErrorsInToast": true,
    "displayLogoImages": true,
    "displayLongDescription": true,
    "displayPersonalSites": true,
    "displayPrivacyScreen": true,
    "displaySiteOrganizations": [],
    "displaySiteOrganizationTypes": [],
    "displaySites": [],
    "displayStatusInToast": false,
    "enableBackNavigation": true,
    "enableTwofaBackNavigation": false,
    "formButtonsDisabledStyle": false,
    "formShowPasswordStyle": "icon",
    "hideSelectCountry": false,
    "hideSiteOrganizations": [],
    "hideSiteOrganizationTypes": [],
    "hideSites": [],
    "oneSiteFlow": false,
    "quickAnswer": false,
    "returnToSiteFormOnUserError": false,
    "saveCredential": true,
    "selectClass": "",
    "socketTimeout": 240000,
    "toastDuration": 5000,
    "toastPosition": "top-right"
  }
}
```

Below are some examples of how you can set up and configure the widget:

---

<br />

##### Example 1: Create a new credential and hide some information

```json
{
  "locale": "es", // Set widget language to Spanish
  // No entrypoint specified: widget will open in CreationCase (create new credential)
  "navigation": {
    "displayBusinessSites": false, // Only show personal sites
    "hideSites": ["Renapo"], // Hide the site 'Renapo'
    "hideSiteOrganizationTypes": ["Blockchain", "Digital Wallet"] // Hide these organization types
  }
}
```

---

<br />

##### Example 2: Open the widget in a specific site and restrict navigation

```json
{
  "locale": "es",
  "entrypoint": {
    "site": "56cf5728784806f72b8b456b" // Open directly in BBVA Bancomer Personal (site ID)
  },
  "navigation": {
    "enableBackNavigation": false // Prevent user from navigating away from this site
  }
}
```

In this case, navigation is restricted so the user cannot move from the specified site. If the user enters credentials for an existing account and the values are valid, the existing credential will be updated.

---

<br />

##### Example 3: Re-synchronize an existing credential

```json
{
  "locale": "es",
  "entrypoint": {
    "credential": "afaf572894806f72b8b4123" // Existing credential ID
  }
}
```

In this example, the widget opens directly in SyncCase for the specified credential, allowing immediate re-synchronization.
