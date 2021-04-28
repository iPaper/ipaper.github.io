---
title: CustomField.SetMultipleCustomFieldValues
permalink: /backend-api/custom-field/set-multiple-custom-field-values
redirect_from: "/display/DOC/SetMultipleCustomFieldValues"
tags: Flipbook Backend API
---

## Description

Sets multiple custom field values in one operation. Values will be validated according to the field datatypes.
The field values are set as a non-atomic operation. That means, if fields A & B are set and field C fails, fields A & B will retain their updated values, while field C will remain unaffected. Likewise, if we're setting fields A, B & C and field B fails, execution will stop there, meaning field C will not have it's value set. Fields will be processed from top to bottom according to the input format.
If a failure occurs, the operation can be run again with correct values. There is no harm in setting a fields value several times with the same value.

## Parameters
<table>
	<thead>
		<tr>
			<th>Name</th>
			<th>Value</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>paperID</td>
			<td>The ID of the iPaper to set values on</td>
		</tr>
		<tr>
			<td>fieldsXml</td>
			<td>
				The field configuration XML that defines the values to set. Sample:
				<pre class="highlight"><code><span class="nt">&lt;fields&gt;</span>
  <span class="nt">&lt;field</span> <span class="na">name=</span><span class="s">"ModelName"</span>&gt;Test<span class="nt">&lt;/field&gt;</span>
  <span class="nt">&lt;field</span> <span class="na">name=</span><span class="s">"ModelYear"</span>&gt;1995<span class="nt">&lt;/field&gt;</span>
<span class="nt">&lt;/fields&gt;</span></code></pre>
			</td>
		</tr>
	</tbody>
</table>

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></ code>
  <message><![CDATA[Custom field values set.]]></message>
</result>
```

## Sample Error Response

If an error occurs in one of the field operations, the field name will be included in the data section.

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[CUSTOMFIELD_FIELD_DOES_NOT_EXIST]]></ code>
  <message><![CDATA[Field 'TestxField' does not exist.]]></message>
  <data>
    <field name="TestxField" />
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