---
title: Paper.GetSettingDescriptions
permalink: /backend-api/paper/get-setting-descriptions
redirect_from: "/display/DOC/GetSettingDescriptions"
tags: Flipbook Backend API
---

## Description

Returns a list of all the settings that can be accessed using the Get/SetSetting methods.

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Setting descriptions retrieved.]]></message>
  <data>
    <settings>
      <setting name="autoMaximize" description="Auto maximize" explanation="Whether the iPaper window should automatically maximize when opened." type="bool" />
      ...
    </settings>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR