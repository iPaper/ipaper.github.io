---
title: Cookie Information
permalink: /technical-information/cookie-information
---

The following cookies are set when visiting a flipbook in the iPaper platform, we put high effort into ensuring that we follow best practises. 

<table>
    <thead>
        <tr>
            <td>Name</td>
            <td>Value</td>
            <td>Purpose</td>
            <td>HttpOnly</td>
            <td>Secure</td>
            <td>Category</td>
            <td>Expiry</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ASP.NET_SessionId</td>
            <td>Unique random string</td>
            <td>Session cookie to ensure that the visitor is given access to the respective flipbook, and it's needed assets.</td>
            <td>True</td>
            <td>True</td>
            <td>Strictly necessary</td>
            <td>Session</td>
        </tr>
        <tr>
            <td>ASP.NET_SessionId_Fallback</td>
            <td>Unique random string</td>
            <td>Fallback session cookie to support older browsers that haven't implemented the Secure flag, in modern evergreen browsers this cookie is never set as it haven't got the Secure flag.</td>
            <td>True</td>
            <td>False</td>
            <td>Strictly necessary</td>
            <td>Session</td>
        </tr>
    </tbody>
</table>