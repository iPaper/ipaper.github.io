---
title: Statistics.GetNumberOfVisitorsPerDay
permalink: /flipbook/backend-api/statistics/get-number-of-visitors-per-day
redirect_from:
  - /backend-api/statistics/get-number-of-visitors-per-day
  - /display/DOC/GetNumberOfVisitorsPerDay
tags: Flipbook Backend API
---

## Description

Returns the number of visitors (based on sessions, not unique visitors) per day, for a Flipbook, in a given time period.

## Parameters

| Name    | Value
|---------|-------------------------------------------------------
| paperID | The ID of the Flipbook to retrieve data from
| from	  | When should data be returned from? Format: YYYY-MM-DD
| to 	  | When should data be returned to? Format: YYYY-MM-DD


## Sample Response
```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Visitor count returned.]]></message>
  <data>
    <visitors>
      <day date="2012-08-15" visitors="47" />
      <day date="2012-08-16" visitors="150" />
      <day date="2012-08-17" visitors="158" />
      <day date="2012-08-18" visitors="155" />
      <day date="2012-08-19" visitors="126" />
      <day date="2012-08-20" visitors="147" />
      <day date="2012-08-21" visitors="146" />
      <day date="2012-08-22" visitors="71" />
      <day date="2012-08-23" visitors="0" />
      <day date="2012-08-24" visitors="0" />
      <day date="2012-08-25" visitors="0" />
    </visitors>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR