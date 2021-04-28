---
title: Paper.MovePaper
permalink: /backend-api/paper/move-paper
redirect_from: "/display/DOC/MovePaper"
tags: Flipbook Backend API
---

## Description

Moves an iPaper (```sourcePaperID```) from it's current parent to a new parent (```destinationParentID```).

## Parameters

| Name                | Value
|---------------------|-------------------------------------------------------------------------
| sourcePaperID       | The ID of the iPaper that should be deleted
| destinationParentID | The ID of the category under which the iPaper/Category should be placed

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Paper moved.]]></message>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* READONLY