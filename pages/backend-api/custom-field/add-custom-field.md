---
title: CustomField.AddCustomField
permalink: /backend-api/custom-field/add-custom-field
redirect_from: "/display/DOC/AddCustomField"
tags: Flipbook Backend API
---

## Description
This method adds a custom field to the list of custom field definitions.

## Parameters
<table>
	<thead>
		<tr>
			<th>Name</th>
			<th>Values</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>name</td>
			<td>The name of the custom field to add. This must be a unique value and match ^[a-zA-Z0-9_]{1,128}$</td>
		</tr>
		<tr>
			<td>dataType</td>
			<td>The data type of the new custom field. Valid values are: <ul><li>datetime</li><li>bool</li><li>int</li><li>string</li></ul></td>
		</tr>
	</tbody>
</table>

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></ code>
  <message><![CDATA[Custom field was added.]]></message>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* READONLY
* CUSTOMFIELD_INVALID_FIELD_NAME
* CUSTOMFIELD_INVALID_DATATYPE
* CUSTOMFIELD_FIELD_NAME_IS_NOT_UNIQUE