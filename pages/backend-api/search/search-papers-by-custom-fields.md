---
title: Search.SearchPapersByCustomField
permalink: /backend-api/search/search-papers-by-custom-fields
redirect_from: "/display/DOC/SearchPapersByCustomFields"
tags: Flipbook Backend API
---

## Description

Searches flipbooks by custom field values.

## Parameters

| Name       | Value
|------------|----------------------------------------------------------------------------------
| categoryID | The category whose descendants should be searched
| xmlOptions | The xmlOptions parameter is used for specifying the search options in XML format


### xmlOptions

* There must be at least one criteria.
* Criteria field values are automatically returned in the customfields section for result papers.
* Any custom fields that should be returned, and are not part of a criteria, should be added to the includedcustomfields section of the options.
* Each custom field criteria will have its value validated according to the field datatype.

**Sample Options**

| Element	 		   | Required | Value
|----------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
| customfieldcriterias | Yes	  | The usewildcards attribute is optional, default is false. Must only be specified for string type custom fields. Wildcard searches can be performed, using % as wildcard character
| includedcustomfields | No 	  | The include all attribute is optional, default is false. Returns all custom field values for the Flipbook. Use with care as amount of data may increase if many fields are defined

```xml
<options>
    <customfieldcriterias>
        <field name="[CriteriaFieldName]" usewildcards="[true/false]" value="[Value]" />
        ...
    </customfieldcriterias>
    <includedcustomfields includeall="[true/false]">
        <field name="[IncludedFieldName]"/>
        ...
    </includedcustomfields>
</options>
```

## Sample Response

{% include note.html content="The lastprocessed field is only included if the Flipbook has been processed. Date is in 24H format." %}
{% include note.html content="The pdffilesize field is only included if the Flipbook has been processed. File size is specified in KB." %}

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Search results returned.]]></message>
  <data>
    <papers>
      <paper id="1120" name="Dot_Matrix_Range" url="/demos/DotMatrixRange/" lastprocessed="2009-03-15 15:27:00" pdffilesize="1357">
        <customfields>
          <field name="TestField" type="int" null="True"><![CDATA[]]></field>
          <field name="date" type="datetime" null="False"><![CDATA[2009-07-25]]></field>
        </customfields>
      </paper>
      ...
    </papers>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* SEARCH_CUSTOMFIELD_DATATYPE_DOES_NOT_SUPPORT_WILDCARDS
* SEARCH_NO_CUSTOM_FIELD_CRITERIAS
* PAPER_DOES_NOT_EXIST
* PAPER_MUST_NOT_BE_CATEGORY