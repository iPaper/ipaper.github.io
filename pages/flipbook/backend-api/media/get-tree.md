---
title: Media.GetTree
permalink: /flipbook/backend-api/media/get-tree
redirect_from:
  - /backend-api/media/get-tree
  - /display/DOC/GetTree
tags: Flipbook Backend API
---

## Description

Returns an XML document listing all directories and files the user has access to. Sizes are in KB.

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></ code>
  <message></message>
  <data>
    <directory directoryid="809" name="PDF">
      <file fileid="127" name="A.pdf" size="17423"/>
      <file fileid="1348" name="B.pdf" size="681323"/>
    </directory>
    <directory directoryid="843" name="Logos"/>
      <directory directoryid="844" name="Client A">
        <file fileid="1348" name="LogoA.jpg" size="109"/>
      </directory>
      <directory directoryid=872" name="Client B">
        <file fileid="2512" name="LogoB.jpg" size="1039"/>
      </directory>
    </directory>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* LOGIN_SECURITY_VIOLATION