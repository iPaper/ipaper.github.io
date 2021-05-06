---
title: Paper.CreatePaper
permalink: /flipbook/backend-api/paper/create-paper
redirect_from:
  - /backend-api/paper/create-paper
  - /display/DOC/CreatePaper
tags: Flipbook Backend API
---

## Description

Creates a paper under the specified parent category id. 

## Parameters

| Name     | Value
|----------|---------------------------------------------------------------------
| parentID | The ID of the category under which the new iPaper should be created
| name	   | The name of the new iPaper
| urlName  | The name of the iPaper as used in URLs

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Paper created.]]></message>
  <data>
    <paper id="1242" />
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* READONLY