---
title: Paper.ClearPublicationPeriod
permalink: /flipbook/backend-api/paper/clear-publication-period
redirect_from:
  - /backend-api/paper/clear-publication-period
  - /display/DOC/ClearPublicationPeriod
tags: Flipbook Backend API
---

## Description

Clears the publication period of a Flipbook, it will always be visible without a publication period.

## Parameters

| Name    | Value
|---------|------------------------------------------------------------------
| paperID | The ID of the Flipbook whose publication period should be changed

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Publication period cleared.]]></message>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* READONLY