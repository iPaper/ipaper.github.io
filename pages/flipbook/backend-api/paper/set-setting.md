---
title: Paper.SetSetting
permalink: /flipbook/backend-api/paper/set-setting
redirect_from: 
  - /backend-api/paper/set-setting
  - /display/DOC/SetSetting
tags: Flipbook Backend API
---

## Description

Sets the specified setting value for the specified PaperID.

## Parameters

| Name    | Value
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------
| paperID | The ID of the iPaper whose setting value should be returned
| setting | The name of the setting whose value should be returned. See [GetSettingDescriptions](/backend-api/paper/get-setting-descriptions.html) for valid setting names
| value   | The value to set. Value will be validated according to the setting type

## Sample Response
```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Setting set.]]></message>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* READONLY