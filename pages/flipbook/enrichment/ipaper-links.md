---
title: iPaper Links
permalink: /flipbook/enrichment/ipaper-links
tags: Flipbook enrichment
---

## Data

Our recommended way of supplying data for the processing of the flipbook is by adding the data as an attached file in the PDF. To reach the end goal in the fastest manner we have a sample CSV embedded in our sample PDF, if that structure is followed it requires close to no customization to get up and running. Besides CSV we currently support Excel, XML, Json and Google Merchant Feed, CSV is preferred for proof of concepts as it's fast to reiterate on.

### Sample CSV Data Structure

The current CSV data format is setup to support current and future enrichment types

<table>
	<thead>
		<tr>
			<th>Column Name</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Id</td>
			<td>Id that is referenced in the {Id} below in the URL Structure</td>
		</tr>
		<tr>
			<td>Description</td>
			<td>Description is used for product description in shop links</td>
		</tr>
		<tr>
			<td>HoverText</td>
			<td>Hovertext will appear when hovering the link in the final flipbook after processing</td>
		</tr>
		<tr>
			<td>HrefTarget</td>
			<td>In the case a url should render as a link type it's possible to control the href target, see <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#target" rel="noopener" target="_blank">MDN Web Docs</a> for reference</td>
		</tr>
		<tr>
			<td>Name</td>
			<td>Name of the product when rendered as a product link</td>
		</tr>
		<tr>
			<td>Url</td>
			<td>Target url when rendering external links</td>
		</tr>
		<tr>
			<td>MediaUrl</td>
			<td>Used for which content should be rendered in Image, Image Popup, Video or Video Popup enrichment types</td>
		</tr>
		<tr>
			<td>Price</td>
			<td>Used as product price when rendering shop links</td>
		</tr>
		<tr>
			<td>AsPopup</td>
			<td>Used to designate if the link should be rendered as a popup frame enrichment type</td>
		</tr>
		<tr>
			<td>PopupFrameMaxWidth</td>
			<td>Controls the width of the popup frame that will be opened from a popup frame enrichment type</td>
		</tr>
		<tr>
			<td>PopupFrameMaxHeight</td>
			<td>Controls the height of the popup frame that will be opened from a popup frame enrichment type</td>
		</tr>
	</tbody>
</table>

## Enrichments

All enrichments should be drawn as hyperlinks in the PDF, where there can only be one click action on the box. The links must be written in accordance to the following specifications. The enrichment in the flipbook will be drawn at the same size of the link box in Adobe PDF.
The hyperlinks for match can be placed in a non-visible layer to ensure that the links doesn't have a negative impact on the looks of the final flipbook.

### URL Structure

* [ipaper://{Behavior}/{Id}]()

### Behaviors

#### ExternalLink

* [ipaper://ExternalLink/{Id}]()
* [ipaper://ExternalLink/{Id}/{AppearanceName}]()

Creates an external link that will be opened in accordance with `HrefTarget` in the data file, if  no value is supplied for `HrefTarget` it will default to `_blank`. The actual will be defined by the `Url` in the data file. In the case a `AsPopup` with the value true is included in the data file this will be rendered as a popup frame inside the flipbook instead of an external link.

#### PageLink

* [ipaper://PageLink/{Id}]()
* [ipaper://PageLink/{Id}/{AppearanceName}]()

To create a link that leads to a different page in the flipbook, in the sample data file you will be able to see that the page value is set in the `Url` column to ensure that there is an alignment between internal an external links.

#### Shop

* [ipaper://Shop/{Id}]()
* [ipaper://Shop/{Id}/{AppearanceName}]()

The `Id` will have to match a product record in the attached datasource, if the product is found a link will be drawn and give the option to add that individual item to the shopping basket of the flipbook for later checkout.
`Id` can consist of characters and letters.

#### Inline Video

* [ipaper://InlineVideo/{Id}]()
* [ipaper://InlineVideo/{Id}/{AppearanceName}]()

This renders the video from `MediaUrl` in the page with the size of the drawn linkbox.

#### Popup Video

* [ipaper://PopupVideo/{Id}]()
* [ipaper://PopupVideo/{Id}/{AppearanceName}]()

Opens the video from `MediaUrl` column in a popup in the flipbook.

#### Inline Image

* [ipaper://InlineImage/{Id}/]()
* [ipaper://InlineImage/{Id}/{AppearanceName}]()

Draws the image from `MediaUrl` column in the page with the size of the link box.

#### Popup Image

* [ipaper://PopupImage/{Id}/]()
* [ipaper://PopupImage/{Id}/{AppearanceName}]()

Opens the image from `MediaUrl` column in a popup

## Enrichment Appearance

Appearance will be defined in the configuration set up in coordinance with Customer Care to ensure the best matching look for the individual customer. In many cases that configuration can be reused as this specification should ensure a certain flow that doesn't need much customization.

Regarding images that is being used for enrichments it will be possible to add files in the pattern `File.ext` as embedded files in the PDF. Valid extensions are PNG, GIF, JPG and SVG.

In the case there are more than one appearance set up in the configuration the `{AppearanceName}` will have to be added to the links to ensure which appearance the individual enrichment will end up with. Besides the name being added to the links, when having multiple files for different appearances the files should be prefixed with `{AppearanceName}-` so the format ends up being `{AppearanceName}-File.ext`
If only one appearance have been configured there is no need for adding it to the urls or the files as we will detect that only one set is present and use that pr. default.

## Sample Enrichment Automation

In the attached sample code this configurations is being used for processing in accordance with the attached PDF. Result of the processing can be seen here: [https://demopartner.ipapercms.dk/sdp/test-enrichmentautomation/]()

```xml
<options>
    <custom-link-import-configuration>
        <EnrichmentAutomation version="1">
	        <Properties>
	            <Id>{$Id}</Id>
	            <HoverText>{$HoverText}</HoverText>
	            <Description>{$Description}</Description>
	            <Url>{$Url}</Url>
	        </Properties>

	        <PdfResource type="iPaperLink" />

	        <Appearance name="Other">
				<!-- PLEASE NOTE THE FILENAME IS WITHOUT THE EXTENSION -->
	            <Icon fileID="{PdfAttachments.File2.Id}">
		            <ScaleFactor>0.1</ScaleFactor>
		            <OffsetX>-10</OffsetX>
		            <OffsetY>-10</OffsetY>
		            <WordOrigin>TopLeft</WordOrigin>
		            <Origin>TopLeft</Origin>
	            </Icon>
	        </Appearance>
            
	        <Appearance>
				<!-- PLEASE NOTE THE FILENAME IS WITHOUT THE EXTENSION -->
	            <Icon fileID="{PdfAttachments.File1.Id}">
		            <ScaleFactor>0.2</ScaleFactor>
		            <OffsetX>-10</OffsetX>
		            <OffsetY>-10</OffsetY>
		            <WordOrigin>TopLeft</WordOrigin>
		            <Origin>TopLeft</Origin>
	            </Icon>
	        </Appearance>
        </EnrichmentAutomation>
    </custom-link-import-configuration>
</options>
```