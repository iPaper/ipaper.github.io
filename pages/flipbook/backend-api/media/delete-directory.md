---
title: Media.DeleteDirectory
permalink: /flipbook/backend-api/media/delete-directory
redirect_from:
  - /backend-api/media/delete-directory
  - /display/DOC/DeleteDirectory
tags: Flipbook Backend API
---

## Description

Deletes a given directory.

## Parameters

| Name        | Value
|-------------|-----------------------------------
| directoryID | The ID of the directory to delete

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code>
    <![CDATA[ SUCCESS ]]>
  </code>
  <message></message>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* LOGIN_SECURITY_VIOLATION