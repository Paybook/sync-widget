## Headless Widget

Headless Widget is a set of functionalities developed by Syncfy that performs specific functions without displaying a graphical user interface to the end user. This is useful if you want to create your own completely customized widget without sacrificing the logic of the Syncfy widget to connect to all supported sites.

## Accessing Headless Widget Methods

All headless methods are available under the `SyncfyWidget.headless` namespace. You do not need to instantiate a new object; simply call the desired method directly from `SyncfyWidget.headless` and pass the required parameters.

**Example usage:**

```js
// Example: Get all countries supported by Syncfy
SyncfyWidget.headless
  .getCountries(authorization, configuration)
  .then((countries) => {
    // Handle the list of countries
  });

// Example: Get a specific site
SyncfyWidget.headless
  .getSite(authorization, id_site, configuration)
  .then((site) => {
    // Handle the site object
  });
```

**Key points:**

- All methods are static and accessed directly from `SyncfyWidget.headless`.
- Most methods return a Promise, so you can use `.then()` or `await` for asynchronous handling.
- Always provide the required parameters as described in each method’s documentation.

---

## Configuration

The **authorization** object is required to authenticate in each of the methods.

```
const authorization={
    // [REQUIRED] A session token obtained from the Syncfy API
    token,
    // [OPTIONAL] you can use the headless widget in strict mode passing the JSON Web Keys
    // JWK(s) as provided in the session object obtained from the Syncfy API:
    strict: {
      authorization,
      body
    },
}
```

The **configuration** object is described below:

```
const configuration={
     // It specifies the widget language. Default='en'. Allowed values: 'en' or 'es'.
  locale: "string",
    // If true, success message will be send when the credentials complete login step
    // in the site. Otherwise, the headless widget will wait to complete all download process.
    // It is exclusively used for the methods:
    // siteConnection() and syncCredential()
    // Default=false
  quickAnswer: "bool",
    // This property specifies the time in milliseconds that the headless widget should
    //wait for the socket.
    // It is exclusively used for the methods:
    // siteConnection() and syncCredential()
    // Default=300000
  socketTimeout: "string",
}
```

## Methods

The SyncfyWidget instance has several methods that you can use, each method will be described below with their respective parameters:

---

### **getCountries**(authorization: Object, configuration: Object)

```
/*
 * Use this method to get all the countries where Syncfy has coverage in connections.
 * This method requires two  parameters: 'authorization' and
 * 'configuration'.
 */
SyncfyWidget.headless.getCountries(authorization, configuration);
```

**Method response example**

```
[
  {
    "id_country": "51ad446a3b8e776312000225",
    "name": "Andorra",
    "code": "AD"
  },
  {
    "id_country": "51ad44da3b8e776312000473",
    "name": "United Arab Emirates",
    "code": "AE"
  },
  {
    "id_country": "51ad44073b8e77631200001c",
    "name": "Afghanistan",
    "code": "AF"
  }...]

```

---

### **getOrganizationSites**(authorization: Object, params: Object, configuration: Object)

```
/*
 * Use this method to get one or more sites from Syncfy's catalog.
 * 'authorization',
 * 'params' ([OPTIONAL] array that allows sending the parameters described below in the request for site filtering)
 * and 'configuration'.
 */
SyncfyWidget.headless.getOrganizationSites(authorization, params, configuration);
```

<br>

**PARAMETERS**

| Parameter                 | Value                                     |
| ------------------------- | ----------------------------------------- |
| id_site_organization      | _ID_ (optional) Site Organization ID      |
| id_site_organization_type | _ID_ (optional) Site Organization Type ID |
| id_country                | _ID_ (optional) Country ID                |
| is_business               | _Number_ (optional) Site is business      |
| is_personal               | _Number_ (optional) Site is personal      |

<br>

**Method response example**

```
[
  {
    "id_site_organization": "5c65e306f9de2a080b61bb31",
    "id_site_organization_type": "56cf4f5b784806cf028b4569",
    "id_country": "51ad446b3b8e77631200022a",
    "name": "AFIP",
    "avatar": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sajBmTElyOEk1cnBiL28ySWpQejJEcHVHMktjYUZpZGZJNEd0V2MxUVE4OUt3RVJIZ0x2VVhLMks4TkxER0lZcnVObk1ab2QvMXI4T2JhSlJmam82RnNBZFBYcmlOcnJ1dz09",
    "small_cover": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sajBmTElyOEk1cnBiL28ySWpQejJEcHVHMktjYUZpZGZISFBjakJSRkl3V2FiYWwzbUY5b2ZFYys4SEZYeVl6RDZLc0V0V3E3cDdyZkx6STlkY0lkMmxmTFZnakJubHhtbzZndTVsWEg4WUVlNjY3TGVsQVlSUT0",
    "cover": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sajBmTElyOEk1cnBiL28ySWpQejJEcHVHMktjYUZpZGZISFBjakJSRkl3V2FiYWwzbUY5b2ZFYys4SEZYeVl6RDZLc0V0V3E3cDdyTjJrdnA0YkloM0UzdEF1TmdTRGJaZz09",
    "sites": [
      {
        "id_site": "5c65e306f9de2a080b61bb32",
        "id_site_type": "5b285177056f2911c13dbce2",
        "is_business": 1,
        "is_personal": 1,
        "version": 3,
        "name": "AFIP Alta usuario",
        "input": [
          {
            "name": "Default",
            "label": "Acceso con Clave Fiscal",
            "fields": [
              {
                "name": "cuit",
                "required": true,
                "type": "text",
                "label": "CUIT",
                "validation": null
              },
              {
                "name": "cuit_contribuyente",
                "required": true,
                "type": "text",
                "label": "CUIT Contribuyente",
                "validation": null
              },
              {
                "name": "password",
                "required": true,
                "type": "password",
                "label": "Clave",
                "validation": null
              }
            ]
          }
        ],
        "endpoint": "/v1/pulls"
      },
      {
        "id_site": "5cf9816af9de2a7ae11c2981",
        "id_site_type": "5b285177056f2911c13dbce1",
        "is_business": 1,
        "is_personal": 1,
        "version": 1,
        "name": "AFIP Mis Comprobantes",
        "credentials": [
          {
            "name": "username",
            "required": true,
            "type": "text",
            "label": "CUIT",
            "validation": null,
            "token": false
          },
          {
            "name": "password",
            "required": true,
            "type": "password",
            "label": "Clave",
            "validation": null,
            "token": false
          }
        ],
        "endpoint": "/v1/credentials"
      },
      {
        "id_site": "5e18e47942eccb2dc5247ce1",
        "id_site_type": "5b285177056f2911c13dbce2",
        "is_business": 1,
        "is_personal": 1,
        "version": 3,
        "name": "AFIP Aceptar Relaciones",
        "input": [
          {
            "name": "Default",
            "label": "Acceso con Clave Fiscal",
            "fields": [
              {
                "name": "cuit",
                "required": true,
                "type": "text",
                "label": "CUIT",
                "validation": null
              },
              {
                "name": "razonsocial",
                "required": true,
                "type": "text",
                "label": "Razón Social",
                "validation": null
              },
              {
                "name": "password",
                "required": true,
                "type": "password",
                "label": "Clave",
                "validation": null
              }
            ]
          }
        ],
        "endpoint": "/v1/pulls"
      },
      {
        "id_site": "614ce4ac3dd5613aab64f4a8",
        "id_site_type": "5b285177056f2911c13dbce2",
        "is_business": 1,
        "is_personal": 1,
        "version": 3,
        "name": "AFIP Alta Usuario V2",
        "input": [
          {
            "name": "Default",
            "label": "Acceso con Clave Fiscal",
            "fields": [
              {
                "name": "cuit_representante",
                "required": true,
                "type": "text",
                "label": "CUIT Representante",
                "validation": null
              },
              {
                "name": "cuit_cliente",
                "required": true,
                "type": "text",
                "label": "CUIT Cliente",
                "validation": null
              },
              {
                "name": "password_cliente",
                "required": true,
                "type": "password",
                "label": "Clave Cliente",
                "validation": null
              },
              {
                "name": "cuit_representado",
                "required": true,
                "type": "text",
                "label": "CUIT Representado",
                "validation": null
              },
              {
                "name": "procesos",
                "required": true,
                "type": "array",
                "label": "Procesos",
                "validation": null
              }
            ]
          }
        ],
        "endpoint": "/v1/pulls"
      }
    ]
  },
    {
      "id_site_organization": "56cf4ff5784806152c8b456a",
      "id_site_organization_type": "56cf4f5b784806cf028b4568",
      "id_country": "51ad44b83b8e7763120003c4",
      "name": "Banamex",
      "avatar": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbFI3bEhOT0JEd2xveDEwNmY3THlZbElDSzFwaFV4S0tPWkdZWXVKZ3o1d1kranh3cEg3Q0RjQ0xUYjRnSDcyNGFyNXIzOHFiV2k3RzhFUlpiQ3l6Tnp1TCtVdUczQXU2Zz09",
      "small_cover": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbFI3bEhOT0JEd2xveDEwNmY3THlZbElDSzFwaFV4S0tGL1dUNndxS0VkWWFya3Z1ZUJuK2VmOVkySnd5eTdiS1k0S0cvM0Z2MkF6L0FRUnBDTmNUUXVSMU1mWjJaUG8xOTNGS2FzUVptRThKaFdzbzdIYUJwUT0",
      "cover": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbFI3bEhOT0JEd2xveDEwNmY3THlZbElDSzFwaFV4S0tGL1dUNndxS0VkWWFya3Z1ZUJuK2VmOVkySnd5eTdiS1k0S0cvM0Z2MkF6c3ZyWi80MHptWm5FUi9GWVBYa2VUdz09",
      "sites": [
        {
          "id_site": "56cf5728784806f72b8b456c",
          "id_site_type": "5b285177056f2911c13dbce1",
          "is_business": 0,
          "is_personal": 1,
          "version": 1,
          "name": "BancaNet Personal",
          "credentials": [
            {
              "name": "username",
              "required": true,
              "type": "text",
              "label": "Número de Cliente",
              "validation": null,
              "token": false
            },
            {
              "name": "password",
              "required": true,
              "type": "password",
              "label": "Contraseña",
              "validation": null,
              "token": false
            }
          ],
          "endpoint": "/v1/credentials"
        },
        {
          "id_site": "571175467848062d698b4568",
          "id_site_type": "5b285177056f2911c13dbce1",
          "is_business": 1,
          "is_personal": 0,
          "version": 1,
          "name": "BancaNet Empresarial",
          "credentials": [
            {
              "name": "username",
              "required": true,
              "type": "text",
              "label": "Usuario",
              "validation": null,
              "token": false
            },
            {
              "name": "password",
              "required": true,
              "type": "password",
              "label": "Contraseña",
              "validation": null,
              "token": false
            }
          ],
          "endpoint": "/v1/credentials"
        }
      ]
    }...]]


```

**NOTE:** The response can vary according to the parameters sent in the configuration.

---

### **getOrganizationTypes**(authorization: Object, configuration: Object)

```
/*
 * Use this method to get all the Organization Types where Syncfy has coverage in connections.
 * This method requires two  parameters: 'authorization' and
 * 'configuration'.
 */
SyncfyWidget.headless.getOrganizationTypes(authorization, configuration);
```

<br>

**Method response example**

```
[
  [
    {
      "id_site_organization_type": "56cf4f5b784806cf028b4568",
      "name": "Bank",
      "label": "webapp_add_banks"
    },
    {
      "id_site_organization_type": "56cf4f5b784806cf028b4569",
      "name": "Government",
      "label": "webapp_add_government"
    },
    {
      "id_site_organization_type": "57fed63a78480609038b4567",
      "name": "Utility",
      "label": "webapp_add_utilities"
    },
    {
      "id_site_organization_type": "57fed63a78480609038b4568",
      "name": "Digital Wallet",
      "label": "webapp_add_wallet"
    },
    {
      "id_site_organization_type": "5b22dcac056f2905f94cdfe1",
      "name": "Blockchain",
      "label": "webapp_add_blockchain"
    }
  ]
]
```

**NOTE:** The response can vary according to the parameters sent in the configuration.

---

### **getSite**(authorization: Object, id_site: String, configuration: Object)

```
/*
 * Use this method to get a specific site.
 * This method requires three parameters:
 * 'authorization',
 * 'id_site' (site ID) and
 * 'configuration'.
 */
SyncfyWidget.headless.getSite(authorization, id_site, configuration);
```

<br>

**Method response example**

```
[
  {
    "id_site": "571175467848062d698b4568",
    "id_site_type": "5b285177056f2911c13dbce1",
    "is_business": 1,
    "is_personal": 0,
    "name": "BancaNet Empresarial",
    "credentials": [
      {
        "name": "username",
        "required": true,
        "type": "text",
        "label": "Usuario",
        "validation": null,
        "token": false
      },
      {
        "name": "password",
        "required": true,
        "type": "password",
        "label": "Contraseña",
        "validation": null,
        "token": false
      }
    ],
    "endpoint": "/v1/credentials",
    "site_organization": {
      "id_site_organization": "56cf4ff5784806152c8b456a",
      "id_site_organization_type": "56cf4f5b784806cf028b4568",
      "id_country": "51ad44b83b8e7763120003c4",
      "name": "Banamex",
      "avatar": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbFI3bEhOT0JEd2xveDEwNmY3THlZbElDSzFwaFV4S0tPWkdZWXVKZ3o1d1kranh3cEg3Q0RjQ0xUYjRnSDcyNGFyNXIzOHFiV2k3RzhFUlpiQ3l6Tnp1TCtVdUczQXU2Zz09",
      "small_cover": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbFI3bEhOT0JEd2xveDEwNmY3THlZbElDSzFwaFV4S0tGL1dUNndxS0VkWWFya3Z1ZUJuK2VmOVkySnd5eTdiS1k0S0cvM0Z2MkF6L0FRUnBDTmNUUXVSMU1mWjJaUG8xOTNGS2FzUVptRThKaFdzbzdIYUJwUT0",
      "cover": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbFI3bEhOT0JEd2xveDEwNmY3THlZbElDSzFwaFV4S0tGL1dUNndxS0VkWWFya3Z1ZUJuK2VmOVkySnd5eTdiS1k0S0cvM0Z2MkF6c3ZyWi80MHptWm5FUi9GWVBYa2VUdz09"
    },
    "version": 1
  }
]

```

---

### **siteConnection**(authorization: Object, site Object, configuration: Object)

<br>

This method returns a promise that resolves to an object. This object has different methods and events that can be used according to your needs:
<br>

```
/*
 * Use this method to connect a specific site.
 * This method requires three parameters:
 * 'authorization',
 * 'site' (Object obtained from the getSite() method)
 * and 'configuration'.
 */
SyncfyWidget.headless.siteConnection(authorization, site, configuration);
```

<br>

#### **siteConnection Methods**

##### **getFields**()

This method is used for V1 sites.

```
/*
 * Use this method to get the fields of the requested site.
 * This method is for version 1 sites.
 */
 SyncfyWidget.headless
      .getSite(authorization, id_site, configuration)
      .then((apiSite) => {
        SyncfyWidget.headless
          .siteConnection(authorization, apiSite, configuration)
          .then((site) => {
              if (site.version === 1) {
                site.getFields();
              }
          });
      })
```

**Method response example**

```
[
  {
    "name": "username",
    "required": true,
    "type": "text",
    "label": "Usuario",
    "validation": null,
    "token": false
  },
  {
    "name": "password",
    "required": true,
    "type": "password",
    "label": "Contraseña",
    "validation": null,
    "token": false
  }
]
```

**NOTE:** The response varies according to the requested site.

<br>

##### **getFields**(index)

This method is used for V3 sites.

```
/*
 * Use this method to get the fields of the requested site.
 * This method is for version 3 sites.
 */
 SyncfyWidget.headless
      .getSite(authorization, id_site, configuration)
      .then((apiSite) => {
        SyncfyWidget.headless
          .siteConnection(authorization, apiSite, configuration)
          .then((site) => {
              if (site.version === 3) {
                site.getFields(0);
              }
          });
      })
```

**Method response example**

```
[
  {
    "name": "rfc",
    "required": true,
    "type": "text",
    "label": "RFC",
    "validation": null
  },
  {
    "name": "password",
    "required": true,
    "type": "password",
    "label": "Contraseña",
    "validation": null
  }
]
```

**NOTE:** The response varies according to the requested site.

<br>

##### **getFields**(index, updateMode = false)

This method is used for V4 sites.

```
/*
 * Use this method to get the fields of the requested site.
 * This method is for version 4 sites.
 * If updateMode is true, only non-identifier fields are returned (for updateCredential flows).
 */
SyncfyWidget.headless
  .getSite(authorization, id_site, configuration)
  .then((apiSite) => {
    SyncfyWidget.headless
      .siteConnection(authorization, apiSite, configuration)
      .then((site) => {
        if (site.version === 4) {
          // For connection (all fields):
          site.getFields(0);
          // For update (only updatable fields):
          site.getFields(0, true);
        }
      });
  });
```

**Method response example**

```
[
  {
    "name": "username",
    "required": true,
    "type": "text",
    "label": "Usuario",
    "validation": null,
    "identifier": true
  },
  {
    "name": "password",
    "required": true,
    "type": "password",
    "label": "Contraseña",
    "validation": null,
    "identifier": false
  }
]
```

**NOTE:** The response varies according to the requested site and the `updateMode` flag.

<br>

##### **getBackUpFields**(updateMode = false)

This method is used for V4 sites that support a backup connection flow.

```
/*
 * Use this method to get the backup fields of the requested site.
 * This method is for version 4 sites.
 * If updateMode is true, only non-identifier fields are returned (for updateCredential flows).
 */
SyncfyWidget.headless
  .getSite(authorization, id_site, configuration)
  .then((apiSite) => {
    SyncfyWidget.headless
      .siteConnection(authorization, apiSite, configuration)
      .then((site) => {
        if (site.version === 4) {
          // For connection (all backup fields):
          site.getBackUpFields();
          // For update (only updatable backup fields):
          site.getBackUpFields(true);
        }
      });
  });
```

**Method response example**

```
[
  {
    "name": "statement_file",
    "required": true,
    "type": "file",
    "label": "Estado de cuenta",
    "validation": null,
    "identifier": false
  }
]
```

**NOTE:** The response varies according to the requested site and the `updateMode` flag.

<br>

##### **getOptions**()

This method is used for V3 or V4 sites.

```
/*
 * Use this method to get the options of the requested site.
 * This method is for version 3 sites.
 */
 SyncfyWidget.headless
      .getSite(authorization, id_site, configuration)
      .then((apiSite) => {
        SyncfyWidget.headless
          .siteConnection(authorization, apiSite, configuration)
          .then((site) => {
              if (site.version === 3 || site.version === 4) {
                site.getOptions();
              }
          });
      })
```

**Method response example**

```
[
  {
    "name": "Default",
    "label": "Acceso por Contraseña",
    "fields": [
      {
        "name": "rfc",
        "required": true,
        "type": "text",
        "label": "RFC",
        "validation": null
      },
      {
        "name": "password",
        "required": true,
        "type": "password",
        "label": "Contraseña",
        "validation": null
      }
    ]
  }
]
```

**NOTE:** The response varies according to the requested site.

<br>

##### **connect**(data)

This method is used for V1 sites.

```
/*
 * Use this method to send the access credentials and establish a connection to the site.
 * This method is for version 1 sites.
 * The JSON containing the access credentials (data), for example: {'username':'test', 'password':'test'}, is sent as a parameter.
 */
if (site.version === 1) {
      site.connect(data);
  }
```

<br>

##### **connect**(index, data)

This method is used for V3 sites.

```
/*
 * Use this method to send the access credentials and establish a connection to the site.
 * This method is for version 3 sites.
 * The JSON containing the access credentials (data), for example: {'username':'test', 'password':'test'}, is sent as a parameter.
 */
if (site.version === 3) {
      site.connect(0, data);
  }
```

##### **connect**(index, data, backUp = false)

This method is used for V4 sites.

```
/*
 * Use this method to send the access credentials and establish a connection to the site.
 * This method is for version 4 sites.
 * The index parameter selects the connection option (from getOptions()).
 * The data parameter is an object with the required fields.
 * The backUp parameter (default: false) triggers the backup flow if true.
 */
if (site.version === 4) {
  // Normal connection
  site.connect(0, { username: "user", password: "pass" });
  // Backup connection (e.g., statement upload)
  site.connect(0, { statement_file: /* file object */ }, true);
}
```

<br>

#### **siteConnection Events**

The list of events available is described below:

##### **on**('twofa', ... )

```
SyncfyWidget.headless
      .getSite(authorization, id_site, configuration)
      .then((apiSite) => {
        SyncfyWidget.headless
          .siteConnection(authorization, apiSite, configuration)
          .then((site) => {
                site.on('twofa', () => {
                // ... do something if a 410 is detected in the credential status, indicating that two-factor authentication is required
          });
      })
```

<br>

##### **on**('socket-quick-answer', ... )

```
SyncfyWidget.headless
      .getSite(authorization, id_site, configuration)
      .then((apiSite) => {
        SyncfyWidget.headless
          .siteConnection(authorization, apiSite, configuration)
          .then((site) => {
                site.on('socket-quick-answer', () => {
                // ... do something if the configuration has 'quick answer' enabled and the credentials successfully log in.
              });
      })
```

<br>

##### **on**('socket-timeout', ... )

```
SyncfyWidget.headless
      .getSite(authorization, id_site, configuration)
      .then((apiSite) => {
        SyncfyWidget.headless
          .siteConnection(authorization, apiSite, configuration)
          .then((site) => {
                site.on('socket-timeout', () => {
                // ... do something if the socketTimeout time has elapsed.
              });
      })
```

<br>

##### **on**('login-success', ...)

```
SyncfyWidget.headless
      .getSite(authorization, id_site, configuration)
      .then((apiSite) => {
        SyncfyWidget.headless
          .siteConnection(authorization, apiSite, configuration)
          .then((site) => {
            site.on('login-success', () => {
                // ... do something when the access credentials are successfully sent via API ...
            });
          });
      })
```

<br>

##### **on**('socket-message', ... )

```
SyncfyWidget.headless
      .getSite(authorization, id_site, configuration)
      .then((apiSite) => {
        SyncfyWidget.headless
          .siteConnection(authorization, apiSite, configuration)
          .then((site) => {
            site.on('socket-message', (CredentialStatus) => {
                /*
                * In particular, this event is triggered while the synchronization status
                * is running and after each change in the synchronization status this
                * event is triggered with the current's status data
                ... do something when a new synchronization status is reached ...
                */
            });
          });
      })
```

**CredentialStatus value:**

```
{
    "code": "Number"
}
```

<br>

##### **on**('status-updated', ...)

```
SyncfyWidget.headless
      .getSite(authorization, id_site, configuration)
      .then((apiSite) => {
        SyncfyWidget.headless
          .siteConnection(authorization, apiSite, configuration)
          .then((site) => {
              site.on('status-updated', (newStatus) => {
                  //... do something depending on the updated state ...
              });
          });
      })
```

**newStatus value:**

| Status          | Description                                                      |
| --------------- | ---------------------------------------------------------------- |
| "start"         | The synchronization has started                                  |
| "loading"       | The synchronization is loading                                   |
| "twofa"         | Code 410 detected, requires two-factor authentication (2FA)      |
| "twofa-loading" | The two-factor authentication (2FA) has been sent and is loading |
| "finish"        | The synchronization has finished                                 |

---

### **syncCredential**(authorization: Object, id_credential: String, configuration: Object)

```
/*
 * Use this method to connect a specific credential.
 * This method requires three parameters
 * 'authorization',
 * 'id_credential' (Syncfy credential ID) and
 * 'configuration'.
 */
SyncfyWidget.headless.syncCredential(authorization,id_credential, configuration)
```

<br>

#### **syncCredential Methods**

This method returns a promise that resolves to an object. This object has different methods and events that can be used according to your needs:
<br>

##### **getCredentialData**()

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
            credential.getCredentialData();
        });
```

**Method response example**

```
[
  {
    "id_credential": "64caa2223ec1d1256b7b1d5e",
    "id_user": "6414a9c819d13330660c410f",
    "id_environment": "574894bf7848066d138b4571",
    "id_external": "__QUICKSTART_USER_EXTERNAL_ID__",
    "id_site": "56cf5728784806f72b8b456e",
    "id_site_organization": "56cf4ff5784806152c8b456c",
    "id_site_organization_type": "56cf4f5b784806cf028b4568",
    "id_organization": "56cf4ff5784806152c8b456c",
    "is_authorized": 0,
    "is_disabled": 0,
    "is_locked": 0,
    "is_twofa": 1,
    "can_sync": 1,
    "ready_in": 0,
    "username": "U********a",
    "code": 401,
    "keywords": null,
    "dt_authorized": null,
    "dt_execute": 1691001378,
    "dt_ready": null,
    "dt_refresh": null,
    "dt_disable": null,
    "avatar": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbUthMjRveDk1aE56czMrM05tNzZQRnc1RTNiU1BueHJueTBTaEh2dEF4SDZDMThmWVlmbkZZSzQ1eGgzdGo0SzE1WG9pNUIzL3pBSTB2M2RMaFFoRFc3d2V3Y01FL2xtdz09",
    "cover": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbUthMjRveDk1aE56czMrM05tNzZQRnc1RTNiU1BueHJnQ0prS2hsaEhEcTdQTXNLdmhLWFRVNjRVby82c2x0UUhkWUhUN3A5T29Tcjh0V255OFVJWHFZdjA3b0xuVk9TZz09",
    "name": "Banorte Personal",
    "quickAnswer": false,
    "site": {
      "id_site": "56cf5728784806f72b8b456e",
      "id_site_type": "5b285177056f2911c13dbce1",
      "is_business": 0,
      "is_personal": 1,
      "version": 1,
      "name": "Banorte Personal",
      "credentials": [
        {
          "name": "username",
          "required": true,
          "type": "text",
          "label": "Usuario",
          "validation": null,
          "token": false
        },
        {
          "name": "password",
          "required": true,
          "type": "password",
          "label": "Contraseña",
          "validation": null,
          "token": false
        }
      ],
      "endpoint": "/v1/credentials",
      "organizationSite": {
        "id_site_organization": "56cf4ff5784806152c8b456c",
        "id_site_organization_type": "56cf4f5b784806cf028b4568",
        "id_country": "51ad44b83b8e7763120003c4",
        "name": "Banorte IXE",
        "avatar": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbUthMjRveDk1aE56czMrM05tNzZQRnc1RTNiU1BueHJueTBTaEh2dEF4SDZDMThmWVlmbkZZSzQ1eGgzdGo0SzE1WG9pNUIzL3pBSTB2M2RMaFFoRFc3d2V3Y01FL2xtdz09",
        "small_cover": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbUthMjRveDk1aE56czMrM05tNzZQRnc1RTNiU1BueHJnQ0prS2hsaEhEcTdQTXNLdmhLWFRVNjRVby82c2x0UUhkWUhUN3A5T29TdFVyaW1GNVpNQmlFN3FyZ2ZsRTBCY05TTVVpQWRwcThPQUJrNkw3QWswaz0",
        "cover": "/assets/Z1JLMk5FTTFTcVE4ZW81NWVEZU9sbUthMjRveDk1aE56czMrM05tNzZQRnc1RTNiU1BueHJnQ0prS2hsaEhEcTdQTXNLdmhLWFRVNjRVby82c2x0UUhkWUhUN3A5T29Tcjh0V255OFVJWHFZdjA3b0xuVk9TZz09",
        "sites": [
          {
            "id_site": "56cf5728784806f72b8b456e",
            "id_site_type": "5b285177056f2911c13dbce1",
            "is_business": 0,
            "is_personal": 1,
            "version": 1,
            "name": "Banorte Personal",
            "credentials": [
              {
                "name": "username",
                "required": true,
                "type": "text",
                "label": "Usuario",
                "validation": null,
                "token": false
              },
              {
                "name": "password",
                "required": true,
                "type": "password",
                "label": "Contraseña",
                "validation": null,
                "token": false
              }
            ],
            "endpoint": "/v1/credentials"
          },
          {
            "id_site": "56fd304c78480623038b457b",
            "id_site_type": "5b285177056f2911c13dbce1",
            "is_business": 1,
            "is_personal": 0,
            "version": 1,
            "name": "Banorte en su empresa",
            "credentials": [
              {
                "name": "username",
                "required": true,
                "type": "text",
                "label": "Usuario",
                "validation": null,
                "token": false
              },
              {
                "name": "password",
                "required": true,
                "type": "password",
                "label": "Contraseña",
                "validation": null,
                "token": false
              }
            ],
            "endpoint": "/v1/credentials"
          },
          {
            "id_site": "57accfcd784806f4038b4567",
            "id_site_type": "5b285177056f2911c13dbce1",
            "is_business": 1,
            "is_personal": 0,
            "version": 1,
            "name": "IXE empresa",
            "credentials": [
              {
                "name": "username",
                "required": true,
                "type": "text",
                "label": "Usuario",
                "validation": null,
                "token": false
              },
              {
                "name": "password",
                "required": true,
                "type": "password",
                "label": "Contraseña",
                "validation": null,
                "token": false
              }
            ],
            "endpoint": "/v1/credentials"
          }
        ]
      }
    }
  }
]

```

#### **syncCredential Events**

The list of events available is described below:

##### **on**('found', ... )

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
            credential.on('found', () => {
                // ... do something if the credential exists in the user's credentials.
            });
      })
```

<br>

##### **on**('twofa', ... )

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
            credential.on('twofa', () => {
                // ... do something if a 410 is detected in the credential status, indicating that two-factor authentication is required
                });
      })
```

<br>

##### **on**('socket-quick-answer', ... )

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
            credential.on('socket-quick-answer', () => {
                // ... do something if the configuration has 'quick answer' enabled and the credentials successfully log in.
                });
      })
```

<br>

##### **on**('socket-timeout', ... )

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
            credential.on('socket-timeout', () => {
                // ... do something if the socketTimeout time has elapsed.
                });
      })
```

<br>

##### **on**('socket-error', ...)

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
          credential.on('socket-error', (event) => {
              //... do something when an error occurs in the socket ...
          });
      })
```

<br>

##### **on**('socket-open', ...)

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
        credential.on('socket-open', (event) => {
            //... do something when the socket opens ...
        });
    })
```

<br>

##### **on**('socket-close', ...)

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
        credential.on('socket-close', (event) => {
            //... do something when the socket closes ...
        });
    })
```

<br>

##### **on**('socket-message', ... )

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
            credential.on('socket-message', (CredentialStatus) => {
                /*
                * In particular, this event is triggered while the synchronization status
                * is running and after each change in the synchronization status this
                * event is triggered with the current's status data
                ... do something when a new synchronization status is reached ...
                */
            });
      })
```

**CredentialStatus value:**

```
{
    "code": "Number"
}
```

<br>

##### **on**('status-updated', ...)

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
        credential.on('status-updated', (newStatus) => {
            //... do something when the credential status changes ...
        });
    })
```

**newStatus value:**

| Status                | Description                                                                                     |
| --------------------- | ----------------------------------------------------------------------------------------------- |
| "error"               | There was an error while trying to synchronize the credential                                   |
| "found"               | The credential ID was found in the credentials created by the user                              |
| "not-found"           | The credential ID wasn't found in the credentials created by the user                           |
| "loading"             | The synchronization is loading                                                                  |
| "searching"           | The credential ID is being searched in the credentials created by the user                      |
| "socket-error"        | There was a socket error                                                                        |
| "socket-quick-answer" | The credential successfully logged in to the site, and the quick answer activation was detected |
| "socket-timeout"      | The socket timeout has expired                                                                  |
| "twofa"               | Code 410 detected, requires two-factor authentication (2FA)                                     |
| "twofa-loading"       | The two-factor authentication (2FA) has been sent and is loading                                |
| "twofa-api-error"     | An error was detected in the API regarding the two-factor authentication (2FA)                  |
| "twofa-loading"       | The two-factor authentication (2FA) was sent and is loading                                     |
| "success"             | The synchronization has finished                                                                |

---

## Twofa

There are 3 ways to obtain the same premise for two-factor authentication:

### **twofa**(authorization: Object, status: Object, configuration: Object)

This method returns a promise that resolves to an object. This object has different methods to conclude the credential synchronization with two-factor authentication:

```
/*
 * Use this method to get the two-factor authentication (2FA) object.
 * This method requires three parameters:
 * 'authorization',
 * 'twofaMessage' (Object received when the 'socket-message' event is emitted and status.code is equal to 410)
 * 'id_site' Site's ID
 * and 'configuration'
 */
SyncfyWidget.headless.twofa(authorization, twofaMessage, id_site, configuration)
```

<br>

### **site.twofa**

```
SyncfyWidget.headless
      .getSite(authorization, id_site, configuration)
      .then((apiSite) => {
        SyncfyWidget.headless
          .siteConnection(authorization, apiSite, configuration)
          .then((site) => {
                site.on('twofa', () => {
                site.twofa // ... Use this method to get the two-factor authentication (2FA) object.
                });
      })
```

<br>

### **credential.twofa**

```
SyncfyWidget.headless.syncCredential(authorization, id_credential, configuration)
      .then((credential) => {
            credential.on('twofa', () => {
                credential.twofa // ... Use this method to get the two-factor authentication (2FA) object.
                });
      })
```

### **Twofa properties**

#### **displaySubmitButton**

```
SyncfyWidget.headless
    .twofa(authorization, data, configuration)
        .then((twofa) => {
          twofa.displaySubmitButton; // ... Use this property to determine whether to display the continue button or not ...
      });
```

<br>

### **Twofa methods**

#### **getFields**()

```
SyncfyWidget.headless
    .twofa(authorization, data, configuration)
        .then((twofa) => {
          twofa.getFields();
      });
```

**Method response example**

```
[
    {
      "name": "token",
      "type": "text",
      "label": "Ingrese token:"
    }
 ]
```

<br>

#### **authenticate**(data)

```
/*
 * Use this method to send the two-factor authentication to the site and continue the credential synchronization.
 * The JSON containing the two-factor authentication values (data) is sent as a parameter, for example: {"token": "89704371"}.
 */
      twofa.authenticate(data);

```

### **Twofa Events**

#### **on**('twofa-api-error', ...)

```
  twofa.on('twofa-api-error', () => {
      // ... do something when an error occurs in the API with two-factor authentication ...
  });
```

<br>

#### **on**('twofa-device-error', ...)

```
  twofa.on('twofa-device-error', (error) => {
      //... do something when an error occurs with the two-factor authentication device ...
  });
```

<br>

#### **on**('login-success', ...)

```
  twofa.on('login-success', () => {
      // ... do something when the two-factor authentication is successfully sent via API ...
  });
```

<br>

#### **on**('loading', ...)

```
  twofa.on('loading', () => {
      // ... do something when the two-factor authentication is loading ...
  });
```

---

### **updateCredential**(authorization: Object, id_credential: String, configuration: Object)

```
/*
 * Use this method to update an existing credential.
 * This method requires three parameters:
 * 'authorization',
 * 'id_credential' (Syncfy credential ID), and
 * 'configuration'.
 * Returns a CredentialService instance, which exposes methods and events for the update flow.
 */
SyncfyWidget.headless.updateCredential(authorization, id_credential, configuration);
```

**Parameters:**

- `authorization`: `{ token: string, strict?: object }`
- `id_credential`: `string`
- `configuration`: `{ locale?: string, quickAnswer?: boolean, socketTimeout?: number, ... }`

**Usage example:**

```js
SyncfyWidget.headless
  .updateCredential({ token }, "credential_id", {
    locale: "es",
    quickAnswer: false,
    socketTimeout: 120000,
  })
  .then((credentialService) => {
    credentialService.on("found", () => {
      const site = credentialService.getSite();
      const siteService = credentialService.getSiteService();
      // For v1 sites:
      if (site.version === 1) {
        siteService.getFields(true);
        credentialService.update(siteService, { password: "test" });
      }
      // For v3/v4 sites:
      else if (site.version === 3 || site.version === 4) {
        siteService.getFields(0, true);
        // For backup flow (v4), pass true as the last argument
        credentialService.update(
          siteService,
          { password: "test" },
          0,
          /* backUp */ false
        );
      }
    });
    credentialService.on("twofa", () => {
      // Handle 2FA challenge
      const fields = credentialService.twofa.getFields();
      credentialService.twofa.authenticate({ token: "123456" });
    });
    credentialService.on("socket-message", (data) => {
      // Handle socket status updates
      console.log(data);
    });
    credentialService.on("socket-quick-answer", () => {
      // Handle quick answer event
    });
    credentialService.on("socket-timeout", () => {
      // Handle socket timeout
    });
  });
```

**Notes:**

- The update flow is similar to syncCredential, but is intended for updating credentials non identifier fields.
- For v4 sites, you can use the `backUp` parameter to trigger the backup update flow.
- All events and methods available in the CredentialService instance are also available here.
