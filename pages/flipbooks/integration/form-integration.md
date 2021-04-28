---
title: Form Integration
permalink: /integration/form-integration
redirect_from: "/display/DOC/Form+Integration"
tags: Flipbook
---

## Configuration

When using the Form module, you have to ability enable POST integration. With this setting enabled, when the users clicks the "Submit" button in the Form, the values entered by the user will be sent via a POST request to the endpoint specified under the Form Settings.

The setting needed for enabling POST integration, is shown below:

<img src="/images/form-1.png" style="max-width: 100%; max-height: 100%" />

## Recieving data from Form POST integration

The values recieved by the endpoint, will come in form of standard Web Form values. Each value will have a key corresponding the the "Name" value of the form element. Looking at the overview of your Form, you will a list of all Name of all form fields.

{% include important.html content='Please note that the "Name" value is an internal name not visible by the end-user, as not to confuse with the "Label" value' %}

For the form in the figure beolow, the data recieved by the endpoint would be:

```
Name=Value&Address=Value&Email=Value
```

<img src="/images/form-2.png" style="max-width: 100%; max-height: 100%" />