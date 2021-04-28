---
title: Image.GetImageWith2PxDropShadow
permalink: /flipbook/backend-api/image/get-image-with-2px-drop-shadow
redirect_from:
  - /backend-api/image/get-image-with-2px-drop-shadow
  - /display/DOC/GetImageWith2PxDropShadow
tags: Flipbook Backend API
---

## Description

This method will output the requested image with a 2px drop shadow around it. If successful, the image will be returned directly. If unsucessful, an error will be returned in XML format.

## Parameters

<table>
	<thead>
		<tr>
			<th>Name</th>
			<th>Value</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>pageID</td>
			<td>The PageID of the page whose images should be retrieved</td>
		</tr>
		<tr>
			<td>imageType</td>
			<td>
				The type of image to be retrieved
				<ul>
					<li>Thumb</li>
					<li>Normal</li>
					<li>Zoom</li>
				</ul>
			</td>
		</tr>
	</tbody>
</table>

## Sample Response

*The binary image data will be returned in raw*.

## Sample Error Response

If an error occurs in one of the field operations, the field name will be included in the data section.

## Sample Error Response
```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[ERROR]]></code>
  <message><![CDATA[Unexpected error.]]></message>
</result>
```

## Return Codes

* ERROR