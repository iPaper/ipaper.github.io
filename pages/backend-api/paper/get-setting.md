---
title: Paper.GetSetting
permalink: /backend-api/paper/get-setting
redirect_from: "/display/DOC/GetSetting"
tags: Flipbook Backend API
---

## Description

Returns the specified setting value for the specified PaperID.

## Parameters

| Name    | Value
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------
| paperID | The ID of the iPaper whose setting value should be returned
| setting | The name of the setting whose value should be returned. See [GetSettingDescriptions](/backend-api/paper/get-setting-descriptions.html) for valid setting names

## Sample Response
```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Setting retrieved.]]></message>
  <data>
    <iconPdf><![CDATA[true]]></iconPdf>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR