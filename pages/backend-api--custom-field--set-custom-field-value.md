---
title: CustomField.SetCustomFieldValue
permalink: /backend-api/custom-field/set-custom-field-value
redirect_from: "/display/DOC/SetCustomFieldValue"
tags: Flipbook Backend API
---

## Description

Sets a custom field value for a flipbook

## Parameters

| Name      | Value
|-----------|---------------------------------------------------------------------------
| paperID	| The ID of the flipbooks to set the value on
| fieldName	| The name of the field whose value should be retrieved
| value		| The value to set. Value will be validated according to the field datatype

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
* READONLY
* LOGIN_SECURITY_VIOLATION
* CUSTOMFIELD_FIELD_DOES_NOT_EXIST
* PAPER_DOES_NOT_EXIST
* PAPER_MUST_NOT_BE_CATEGORY
* CUSTOMFIELD_INVALID_DATA_FORMAT