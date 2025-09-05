# Status Codes

These status codes are returned by the Syncfy Widget to indicate the progress, success, errors, or required user actions during credential synchronization.

---

## Credential Status Codes

---

### Progress Information Codes

<table>
    <thead>
        <tr>
            <th colspan="3">1xx</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><b>Code</b></td>
            <td><b>Name</b></td>
            <td><b>Description</b></td>
        </tr>
        <tr>
            <td>100</td>
            <td>Register</td>
            <td>The API registers a new process (through a REST request)</td>
        </tr>
        <tr>
            <td>101</td>
            <td>Starting</td>
            <td>The process information was obtained to start operating</td>
        </tr>
        <tr>
            <td>102</td>
            <td>Running</td>
            <td>The process is running (login successful)</td>
        </tr>
        <tr>
            <td>103</td>
            <td>TokenReceived</td>
            <td>The process received the token</td>
        </tr>
    </tbody>
</table>

---

### Success Codes

<table>
    <thead>
        <tr>
            <th colspan="3">2xx</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><b>Code</b></td>
            <td><b>Name</b></td>
            <td><b>Description</b></td>
        </tr>
        <tr>
            <td>200</td>
            <td>Finish</td>
            <td>The connection has been successful. Data has been extracted.</td>
        </tr>
        <tr>
            <td>201</td>
            <td>Pending</td>
            <td>The connection has been successful. We have partially extracted information, but data will still be extracted in background processes.</td>
        </tr>
        <tr>
            <td>202</td>
            <td>NoTransactions</td>
            <td>The connection has been successful. However, no transactions were found.</td>
        </tr>
        <tr>
            <td>203</td>
            <td>PartialTransactions</td>
            <td>The connection has been successful. However, more than one account does not have transactions.</td>
        </tr>
        <tr>
            <td>204</td>
            <td>Incomplete</td>
            <td>The connection has been successful. However, the data downloaded is incomplete.</td>
        </tr>
        <tr>
            <td>206</td>
            <td>NoAccounts</td>
            <td>The connection has been successful. However, there were no accounts linked to the given credentials.</td>
        </tr>
    </tbody>
</table>

---

### User Interaction Codes

<table>
    <thead>
        <tr>
            <th colspan="3">4xx</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><b>Code</b></td>
            <td><b>Name</b></td>
            <td><b>Description</b></td>
        </tr>
        <tr>
            <td>401</td>
            <td>Unauthorized</td>
            <td>The value of one of the given authentication fields was not accepted by the institution. Please verify the information and try again.</td>
        </tr>
        <tr>
            <td>403</td>
            <td>InvalidToken</td>
            <td>The given token value entered was not accepted by the institution or the expiration time was reached.</td>
        </tr>
        <tr>
            <td>405</td>
            <td>Locked</td>
            <td>The institution has blocked the given credential. Please contact your institution and make sure your connection to the site is working properly before trying again.</td>
        </tr>
        <tr>
            <td>406</td>
            <td>Conflict</td>
            <td>The institution does not allow more than one user to be logged in. If you have logged in to your institution using another device, please make sure to log out before trying again.</td>
        </tr>
        <tr>
            <td>408</td>
            <td>UserAction</td>
            <td>The institution requires attention from the user. We advise you to log in to the institution to confirm everything is working properly. Upon confirmation, try again.</td>
        </tr>
        <tr>
            <td>409</td>
            <td>WrongSite</td>
            <td>The given credentials seem to be valid but they belong to a different site from the same organization.</td>
        </tr>
        <tr>
            <td>449</td>
            <td>DeprecatedSite</td>
            <td>The credential you are trying to sync belongs to a site that is no longer supported.</td>
        </tr>
    </tbody>
</table>

---

### Multi-Factor Authentication Codes

<table>
    <thead>
        <tr>
            <th colspan="3">4xx</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><b>Code</b></td>
            <td><b>Name</b></td>
            <td><b>Description</b></td>
        </tr>
        <tr>
            <td>410</td>
            <td>Waiting</td>
            <td>Waiting for MFA (Multi-Factor Authentication) value from the user.</td>
        </tr>
        <tr>
            <td>411</td>
            <td>TwofaTimeout</td>
            <td>The time to enter the MFA value has been exceeded.</td>
        </tr>
        <tr>
            <td>413</td>
            <td>LoginError</td>
            <td>There is an error in the login process, please try again.</td>
        </tr>
    </tbody>
</table>

---

### Connection Error Codes

<table>
    <thead>
        <tr>
            <th colspan="3">5xx</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><b>Code</b></td>
            <td><b>Name</b></td>
            <td><b>Description</b></td>
        </tr>
        <tr>
            <td>500</td>
            <td>Error</td>
            <td>An internal error has occurred while connecting to the institution.</td>
        </tr>
        <tr>
            <td>501</td>
            <td>Unavailable</td>
            <td>The institution has informed us that there was a problem in the connection. Please wait 15 minutes and try again. If the problem persists, contact Technical Support.</td>
        </tr>
        <tr>
            <td>504</td>
            <td>ConnectionTimeout</td>
            <td>An internal error has occurred while connecting to the institution.</td>
        </tr>
        <tr>
            <td>509</td>
            <td>Undergoing Maintenance</td>
            <td>The institution is under maintenance.</td>
        </tr>
    </tbody>
</table>
