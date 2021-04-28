---
title: Media.UploadFile
permalink: /backend-api/media/upload-file
redirect_from: "/display/DOC/UploadFile"
tags: Flipbook Backend API
---

## Description

Uploads a file to the specified directory.
If the file already exists (matching on the name), it will be overwritten. Otherwise a new file will be created. In either case, the file ID, whether created or updated, will be returned.

## Parameters

| Name       | Value
|------------|---------------------------------------------------------------------------------------------
| parentID   | The ID of the directory into which the file should be uploaded. Use 0 to upload to the root
| name		 | The name of the uploaded file
| base64File | The binary file contents encoded as a base64 string

## Sample Response

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code>
    <![CDATA[ SUCCESS ]]>
  </code>
  <message></message>
  <data>
    <fileid>1583</fileid>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* LOGIN_SECURITY_VIOLATION