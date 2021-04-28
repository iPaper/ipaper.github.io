---
title: Search.SearchPapersByContent
permalink: /flipbook/backend-api/search/search-papers-by-content
redirect_from:
  - /backend-api/search/search-papers-by-content
  - /display/DOC/SearchPapersByContent
tags: Flipbook Backend API
---

## Description

Searches flipbooks recursively for text content on the indexed pages.

## Parameters

| Name              | Value
|-------------------|-------------------------------------------------------------------------------------------------------------
| query    			| The text string to search for. Max length: 128 chars
| categoryOrPaperID | Either a PaperID or a CategoryID that should be searched. Will search recursively if CategoryID is provided
| xmlOptions  		| Not currently used


## Sample Response
```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Search results returned.]]></message>
  <data>
    <results>
      <result paperID="1213" pageNumber="4" paperName="Test Catalog" paperUrl="/Demos/TestCatalog/" />
      <result paperID="1213" pageNumber="5" paperName="Test Catalog" paperUrl="/Demos/TestCatalog/" />
    </results>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* LOGIN_SECURITY_VIOLATION