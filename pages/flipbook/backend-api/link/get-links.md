---
title: Link.GetLinks
permalink: /flipbook/backend-api/link/get-links
redirect_from:
  - /backend-api/link/get-links
  - /display/DOC/GetLinks
tags: Flipbook Backend API
---

## Description
Exports all links from a given iPaper.

{% include note.html content="Superfluous nodes will be removed later on. Thus, for example, a rectangle link will in the future not include the polygoncoords node. When reading the response, you should handle potential missing nodes and degrade gracefully." %}

## Parameters

| Name    | Value
|---------|-----------------------------------------------------
| paperID | The ID of the iPaper whose links should be returned

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></ code>
  <message><![CDATA[Links exported.]]></message>
  <data>
    <root>
      <link number="1">
        <number><![CDATA[2]]></number>
        <x><![CDATA[0.277648839556004]]></x>
        <y><![CDATA[0.231397006414825]]></y>
        <width><![CDATA[0.0671285252555119]]></width>
        <height><![CDATA[0.0132451983038164]]></height>
        <alttext><![CDATA[]]></alttext>
        <url><![CDATA[]]></url>
        <stylename><![CDATA[1']]></stylename>
        <shapetype><![CDATA[rectangle]]></shapetype>
        <polygoncoords><![CDATA[]]></polygoncoords>
        <linktype><![CDATA[shopitem]]></linktype>
        <fileid><![CDATA[]]></fileid>
        <target><![CDATA[]]></target>
        <usemask><![CDATA[True]]></usemask>
        <param><![CDATA[<item><name><![CDATA[FIBERROND. 3M 581C Ø127x22MM P60]]></name><price><![CDATA[2.75]]></price><descr><![CDATA[]]></descr><id><![CDATA[9900002430]]></id></item>]]></param>
      </link>
      <link number="2">
        <number><![CDATA[2]]></number>
        <x><![CDATA[0.114934409687185]]></x>
        <y><![CDATA[0.331147540983607]]></y>
        <width><![CDATA[0.0671285252555116]]></width>
        <height><![CDATA[0.0132451983038164]]></height>
        <alttext><![CDATA[]]></alttext>
        <url><![CDATA[]]></url>
        <stylename><![CDATA[1']]></stylename>
        <shapetype><![CDATA[rectangle]]></shapetype>
        <polygoncoords><![CDATA[]]></polygoncoords>
        <linktype><![CDATA[shopitem]]></linktype>
        <fileid><![CDATA[]]></fileid>
        <target><![CDATA[]]></target>
        <usemask><![CDATA[True]]></usemask>
        <param><![CDATA[<item><name><![CDATA[FIBERROND. 3M 581C Ø127X22MM P50]]></name><price><![CDATA[2.75]]></price><descr><![CDATA[]]></descr><id><![CDATA[9900002429]]></id></item>]]></param>
      </link>
</result>
```

## Return Codes

* SUCCESS
* ERROR