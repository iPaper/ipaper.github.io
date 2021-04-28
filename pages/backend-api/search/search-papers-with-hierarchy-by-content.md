---
title: Search.SearchPapersWithHiearchyByContent
permalink: /backend-api/search/search-papers-with-hierarchy-by-content
redirect_from: "/display/DOC/SearchPapersWithHiearchyByContent"
tags: Flipbook Backend API
---

## Description


Searches Flipbooks recursively for text content on the indexed pages and return Flipbooks with hiearchy information.
## Parameters

| Name       | Value
|------------|-----------------------------------------------------------------
| query    	 | The text string to search for. Max length: 128 chars
| categoryID | The CategoryID that should be searched. Will search recursively
| xmlOptions | Not currently used


## Sample Response
```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Search results returned.]]></message>
  <data>
    <papers>
      <paper paperID="4984" name="MyPaper" url="/Client1/MyPaper/" parentID="3629" category="False" />
      <paper paperID="4985" name="Category1" url="/Client1/Category1/" parentID="3629" category="True" />
      <paper paperID="4986" name="NewPaper" url="/Client/Category1/NewPaper/" parentID="4985" category="False" />
    </papers>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* LOGIN_SECURITY_VIOLATION