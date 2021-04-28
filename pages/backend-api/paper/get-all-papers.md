---
title: Paper.GetAllPapers
permalink: /backend-api/paper/get-all-papers
redirect_from: "/display/DOC/GetAllPapers"
tags: Flipbook Backend API
---

## Description

Returns an XML document listing all categories and iPapers below, and including, the requested PaperID. If a publication period restriction is set on the iPaper, the publicationperiod-from and publicationperiod-to fields will be present.

## Parameters

| Name     | Value
|----------|------------------------------------------------------------------------------------
| paperID  | The ID of the iPaper that should be the root level of the tree of iPapers returned

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[List of papers retrieved.]]></message>
  <data>
    <category id="182" name="Partner" url="/">
      <category id="173" name="Demos" url="/demos/">
        <category id="1240" name="hep23" url="/demos/hep23/" />
        <paper id="1106" name="21" url="/demos/21/" />
        <paper id="1114" name="CC" url="/demos/CC/" />
        <paper id="1120" name="Dot_Matrix_Range" url="/demos/Dot_Matrix_range/" publicationperiod-from="2014-05-14 01:25:00" publicationperiod-to="2014-05-29 01:35:00" />
        <paper id="1117" name="edc" url="/demos/edc/" />
        <paper id="1233" name="ipaper" url="/demos/ipaper/" />
        <paper id="1232" name="Test" url="/demos/Test/" />
      </category>
    </category>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR