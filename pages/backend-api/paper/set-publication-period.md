---
title: Paper.SetPublicationPeriod
permalink: /backend-api/paper/set-publication-period
redirect_from: "/display/DOC/SetPublicationPeriod"
tags: Flipbook Backend API
---

## Description

Clears the publication period of an iPaper, it will always be visible without a publication period.

## Parameters

| Name    | Value
|---------|----------------------------------------------------------------
| paperID | The ID of the iPaper whose publication period should be changed
| from	  | The beginning of the publication period
| to      | The end of the publication period

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