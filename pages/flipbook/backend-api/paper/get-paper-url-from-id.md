---
title: Paper.GetPaperUrlFromID
permalink: /flipbook/backend-api/paper/get-paper-url-from-id
redirect_from:
  - /backend-api/paper/get-paper-url-from-id
  - /display/DOC/GetPaperUrlFromID
tags: Flipbook Backend API
---

## Description

Returns the url of an iPaper, given its ID.

## Parameters

| Name               | Value
|--------------------|---------------------------------------------------
| paperID            | The ID of the iPaper whose URL should be returned

## Sample Response (iPaper Found)

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Paper found.]]></message>
  <data>
    <paper url="/demos/21/" />
  </data>
</result>
```

## Sample Response (iPaper Not Found)

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[PAPER_DOES_NOT_EXIST]]></code>
  <message><![CDATA[Paper not found.]]></message>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* PAPER_DOES_NOT_EXIST