---
title: CustomField.GetCustomFieldValue
permalink: /backend-api/custom-field/get-custom-field-value
redirect_from: "/display/DOC/GetCustomFieldValue"
tags: Flipbook Backend API
---

## Description

Retrieves a list of defined custom fields.

## Parameters

| Name      | Value
|-----------|------------------------------------------------------------------
| paperID   | The ID of the iPaper for which a field value should be retrieved
| fieldName | The name of the field whose value should be retrieved

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