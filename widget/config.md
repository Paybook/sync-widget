# Syncfy Widget: Set Up and Configuration

---

## How to set up or instantiate the Syncfy Widget?

1. **Add an HTML element** where you want the widget to appear:

   ```html
   <div id="widget"></div>
   ```

   > The widget will be appended inside this element. The `id` or selector you use must match the `element` parameter when instantiating the widget.

2. **Instantiate the widget** in your JavaScript code:

   ```javascript
   import SyncfyWidget from "@syncfy/authentication-widget";

   const params = {
     token, // [REQUIRED] A session token obtained from the Syncfy API
     element: "#widget", // [REQUIRED] DOM selector or Element instance
     config: {
       /* WidgetConfig object, see below */
     },
     enableTestMode: false, // [OPTIONAL] Enable test mode
     refreshTokenFunction: () => Promise.resolve({ token: "..." }), // [OPTIONAL]
   };

   const syncfyWidget = new SyncfyWidget(params);
   syncfyWidget.open();
   ```

---

## Parameters

| **Parameter**            |      **Type**       | **Required** | **Default Value** | **Description**                                                                                 |
| ------------------------ | :-----------------: | :----------: | :---------------: | :---------------------------------------------------------------------------------------------- |
| `token`                  |     **String**      |     Yes      |         —         | A valid Syncfy API token (Sandbox or Production).                                               |
| `element`                | **String, Element** |     Yes      |    `"#widget"`    | DOM selector or Element where the widget will be rendered.                                      |
| `config`                 |  **WidgetConfig**   |      No      | See table below.  | Widget configuration object (see below).                                                        |
| `enableTestMode`         |     **Boolean**     |      No      |      `false`      | Enable widget test mode.                                                                        |
| `refreshTokenFunction()` |    **Function**     |      No      |    `undefined`    | Function returning a Promise with `{ token: String, strict?: Object }`. Used for token refresh. |

---

## WidgetConfig Object

The `config` parameter is a **WidgetConfig** object. Here are the main attributes:

| **Attribute**                             |     **Type**      | **Default Value** | **Description**                                                                                        |
| ----------------------------------------- | :---------------: | :---------------: | :----------------------------------------------------------------------------------------------------- |
| `client`                                  |    **Object**     |       `{}`        | Information about the client (branding, logo, name).                                                   |
| `client.logo`                             |    **String**     |         —         | URL for the client logo.                                                                               |
| `client.name`                             |    **String**     |         —         | Client name to display.                                                                                |
| `entrypoint`                              |    **Object**     |       `{}`        | Where the widget starts (country, credential, site, etc).                                              |
| `entrypoint.country`                      |    **String**     |      `"MX"`       | ISO country code. Opens widget in CreationCase for the given country.                                  |
| `entrypoint.credential`                   |    **String**     |      `null`       | Opens widget in SyncCase for the given credential.                                                     |
| `entrypoint.site`                         |    **String**     |      `null`       | Opens widget in UpdateCase for the given site.                                                         |
| `entrypoint.siteOrganizationType`         |    **String**     |      `null`       | Opens widget in CreationCase and selects the given site organization type.                             |
| `entrypoint.updateCredential`             |    **String**     |      `null`       | Opens widget in UpdateCase for the given credential, showing only non-identifier fields.               |
| `locale`                                  |    **String**     |      `"en"`       | Widget language (`"en"` or `"es"`).                                                                    |
| `navigation`                              |    **Object**     |       `{}`        | Navigation and UI settings (see below).                                                                |
| `navigation.disableFormAutocomplete`      |    **Boolean**    |      `false`      | Disable browser form autocomplete.                                                                     |
| `navigation.displayBusinessSites`         |    **Boolean**    |      `true`       | Show all business sites.                                                                               |
| `navigation.displayCredentialInModal`     |    **Boolean**    |      `false`      | Show credential process in toast (`true`) or modal (`false`).                                          |
| `navigation.displayErrorsInToast`         |    **Boolean**    |      `true`       | Show errors in toast (`true`) or modal (`false`).                                                      |
| `navigation.displayLogoImages`            |    **Boolean**    |      `true`       | Show logos for sites, organizations, and status toasts.                                                |
| `navigation.displayLongDescription`       |    **Boolean**    |      `true`       | Expand status toast to show long description on final status.                                          |
| `navigation.displayPersonalSites`         |    **Boolean**    |      `true`       | Show all personal sites.                                                                               |
| `navigation.displayPrivacyScreen`         |    **Boolean**    |      `true`       | Show privacy policy screen before syncing.                                                             |
| `navigation.displaySiteOrganizations`     | **Array<String>** |       `[]`        | Show only the specified site organizations.                                                            |
| `navigation.displaySiteOrganizationTypes` | **Array<String>** |       `[]`        | Show only the specified site organization types.                                                       |
| `navigation.displaySites`                 | **Array<String>** |       `[]`        | Show only the specified sites.                                                                         |
| `navigation.displayStatusInToast`         |    **Boolean**    |      `false`      | Continue process in toast after modal closes.                                                          |
| `navigation.enableBackNavigation`         |    **Boolean**    |      `true`       | Show back buttons in side menu and credential input form.                                              |
| `navigation.enableTwofaBackNavigation`    |    **Boolean**    |      `false`      | Show back button in two-factor authentication form.                                                    |
| `navigation.formButtonsDisabledStyle`     |    **Boolean**    |      `false`      | Disable submit buttons when form is invalid.                                                           |
| `navigation.formShowPasswordStyle`        |    **String**     |      `icon`       | Show/hide password: `icon`, `text`, or `none`.                                                         |
| `navigation.hideAsideMenu`                |    **Boolean**    |      `false`      | Hide the aside menu.                                                                                   |
| `navigation.hideSelectCountry`            |    **Boolean**    |      `false`      | Hide the select country input.                                                                         |
| `navigation.hideSiteOrganizations`        | **Array<String>** |       `[]`        | Hide the specified site organizations.                                                                 |
| `navigation.hideSiteOrganizationTypes`    | **Array<String>** |       `[]`        | Hide the specified site organization types.                                                            |
| `navigation.hideSites`                    | **Array<String>** |       `[]`        | Hide the specified sites.                                                                              |
| `navigation.oneSiteFlow`                  |    **Boolean**    |      `false`      | If true and `entrypoint.site` is set, user flow starts and ends in that site.                          |
| `navigation.quickAnswer`                  |    **Boolean**    |      `false`      | Show final status after authentication, or wait for data download.                                     |
| `navigation.returnToSiteFormOnUserError`  | **Boolean/Array** |      `false`      | Return to site form on user error (or for specific error codes).                                       |
| `navigation.saveCredential`               |    **Boolean**    |      `true`       | Save credential data for future connections.                                                           |
| `navigation.selectClass`                  |    **String**     |       `""`        | Class to append to all select dropdowns.                                                               |
| `navigation.socketTimeout`                |    **Number**     |     `240000`      | Duration (ms) before socket times out.                                                                 |
| `navigation.toastDuration`                |    **Number**     |      `5000`       | Duration (ms) to keep status toast open on success.                                                    |
| `navigation.toastPosition`                |    **String**     |    `top-right`    | Toast position: `top-left`, `top-center`, `top-right`, `bottom-left`, `bottom-center`, `bottom-right`. |

---

### Notes

- If any configuration attribute value is invalid, the widget will throw an exception and not display.
- If an entrypoint attribute value is invalid (e.g., a site ID not found in the Syncfy API), the widget will throw an exception and not display data.
- For entrypoint attributes, `credential` takes precedence over `site` if both are provided.
