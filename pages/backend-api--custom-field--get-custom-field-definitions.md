---
title: CustomField.GetCustomFieldDefinitions
permalink: /backend-api/custom-field/get-custom-field-definitions
redirect_from: "/display/DOC/GetCustomFieldDefinitions"
tags: Flipbook Backend API
---

## Description
Retrieves a list of defined custom fields.

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></ code>
  <message><![CDATA[Custom fields retrieved.]]></message>
  <data>
    <fields>
      <field name="date" datatype="datetime" />
      <field name="FieldName" datatype="string" />
      <field name="TestField" datatype="int" />
      ...
    </fields>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR