---
title: Paper.GetPaperIDFromUrl
permalink: /flipbook/backend-api/paper/get-paper-id-from-url
redirect_from:
  - /backend-api/paper/get-paper-id-from-url
  - /display/DOC/GetPaperIDFromUrl
tags: Flipbook Backend API
---

## Description

Returns the ID of an iPaper, given its url. Can also be used to check whether a url is vacant.

## Parameters

| Name  | Value
|-------|---------------------------------------------------------------------------------------------------------
| url   | The URL of the iPaper whose ID should be returned. Url must start with a ```/``` and end with a ```/```

## Sample Response When iPaper Not Found

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Paper not found.]]></message>
</result>
```

## Sample Response When iPaper Is Found

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Paper found.]]></message>
  <data>
    <paper id="1106" />
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR