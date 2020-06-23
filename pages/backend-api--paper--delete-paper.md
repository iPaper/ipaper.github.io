---
title: Paper.DeletePaper
permalink: /backend-api/paper/delete-paper
redirect_from: "/display/DOC/DeletePaper"
tags: Flipbook Backend API
---

## Description

Deletes the specified paper.

## Parameters

| Name     | Value
|----------|--------------------------------------------
| paperID  | The ID of the iPaper that should be deleted

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Paper deleted.]]></message>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* READONLY