---
title: Ripper.GetProcessingPapers
permalink: /flipbook/backend-api/ripper/get-processing-papers
redirect_from:
  - /backend-api/ripper/get-processing-papers
  - /display/DOC/GetProcessingPapers
tags: Flipbook Backend API
---

## Description

Returns a list of Flipbooks currently being processed.

## Sample Response
```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[List retrieved successfully.]]></message>
  <data>
    <processes>
      <process created="2009-03-16 18:00:07" paper-id="1120" progress="0" />
    </processes>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR