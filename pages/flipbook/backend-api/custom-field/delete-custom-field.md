---
title: CustomField.DeleteCustomField
permalink: /flipbook/backend-api/custom-field/delete-custom-field
redirect_from:
  - /backend-api/custom-field/delete-custom-field
  - /display/DOC/DeleteCustomField
tags: Flipbook Backend API
---

## Description
This method deletes a custom field from the list of custom field definitions.

## Parameters

| Name | Value
|------|-------
| name | The name of the field to be deleted

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></ code>
  <message><![CDATA[Field was deleted.]]></message>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* READONLY
* CUSTOMFIELD_FIELD_DOES_NOT_EXIST