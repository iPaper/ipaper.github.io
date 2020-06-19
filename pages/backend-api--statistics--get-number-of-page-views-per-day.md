---
title: Statistics.GetNumberOfPageviewsPerDay
permalink: /backend-api/statistics/get-number-of-page-views-per-day
redirect_from: "/display/DOC/GetNumberOfPageviewsPerDay"
tags: Flipbook Backend API
---

## Description

Returns the number of pageviews per day, for a Flipbook, in a given time period.

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
  <message />
  <data>
    <pageviews>
      <day date="2012-01-28" views="0" />
      <day date="2012-01-29" views="0" />
      <day date="2012-01-30" views="0" />
      <day date="2012-01-31" views="0" />
      <day date="2012-02-01" views="0" />
      <day date="2012-02-02" views="16" />
      <day date="2012-02-03" views="0" />
      <day date="2012-02-04" views="0" />
      <day date="2012-02-05" views="0" />
    </pageviews>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR