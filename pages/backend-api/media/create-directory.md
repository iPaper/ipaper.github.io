---
title: Media.CreateDirectory
permalink: /backend-api/media/create-directory
redirect_from: "/display/DOC/CreateDirectory"
tags: Flipbook Backend API
---

## Description

Creates a directory at the specified location.

## Parameters

| Name      | Value
|-----------|---------------------------------------------------------------------------
| parentID	| The ID of the parent directory. Use 0 to create a directory in the root
| name		| The name of the field whose value should be retrieved

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code>
    <![CDATA[ SUCCESS ]]>
  </code>
  <message></message>
  <data>
    <directoryid>948</directoryid>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* LOGIN_SECURITY_VIOLATION