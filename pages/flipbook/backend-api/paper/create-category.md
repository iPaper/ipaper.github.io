---
title: Paper.CreateCategory
permalink: /flipbook/backend-api/paper/create-category
redirect_from:
  - /backend-api/paper/create-category
  - /display/DOC/CreateCategory
tags: Flipbook Backend API
---

## Description

Creates a category under the specified parent category id.

## Parameters

| Name    | Value
|---------|----------------------------------------------------------------
| paperID | The ID of the iPaper whose publication period should be changed
| name	  | The name of the new category
| urlName | The name of the category as used in URLs

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Category created.]]></message>
  <data>
    <paper id="1240" />
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* READONLY