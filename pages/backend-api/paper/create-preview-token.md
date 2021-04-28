---
title: Paper.CreatePreviewToken
permalink: /backend-api/paper/create-preview-token
redirect_from: "/display/DOC/CreatePreviewToken"
tags: Flipbook Backend API
---

## Description

Creates a preview SecurityToken that can be used to bypass any security on the Flipbook. After creating a token for a specific Flipbook, a specific client IP address and for a given time period, the Flipbook may be accessed using the URL: ```<urlToFlipbook>/?SecurityToken=<token>``` to bypass any security. This is typically used for scenarios where the user is logged in to an intranet and does not want to login to see the Flipbooks, while Flipbooks should be protected from public viewing.
Instead of linking directly to the Flipbooks from the intranet, the intranet should link to a local page that creates the securitytoken and then redirects the user to the catalog.

Typical workflow:

1. [Intranet] User clicks link to Flipbook.
2. [Intranet] Requests security token from iPaper.
3. [iPaper] Security token created & returned.
4. [Intranet] Redirects user to actual Flipbook with securitytoken appended

## Parameters

| Name            | Value
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------
| paperID         | The ID of the iPaper that should be granted access to
| validityMinutes | How long the security token should be valid for
| ip              | The IP that should be granted access. If this is en empty string, no IP validation will be performed and any IP presenting the correct token will be granted access

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Preview token created.]]></message>
  <data>
    <token><![CDATA[ffc8d256-c727-4bc7-9a32-67a929f4fa53]]></token>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* LOGIN_SECURITY_VIOLATION