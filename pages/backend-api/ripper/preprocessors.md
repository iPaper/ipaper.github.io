---
title: Ripper Preprocessors
permalink: /backend-api/ripper/preprocessors
redirect_from: "/display/DOC/Watermark"
tags: Flipbook Backend API
---

## Watermark

### Description

Can be used to automatically imprint a watermark text on pages of a PDF during processing. The text will be placed in the bottom left corner of all pages. By setting the opacity to 0 it's possible to insert an invisible watermark that can only be found through search or saving the PDF in text format.

### XML Options

| Name 			  | Required | Datatype 		 | Description
|-----------------|----------|-------------------|---------------------------------------------------------------------------------------
| text 			  | Yes 	 | string   		 | The text to be imprinted on the pages
| opacity 		  | Yes 	 | float (0.0 - 1.0) | The opacity of the text
| font-size 	  | Yes 	 | int 				 | The font size of the text
| only-first-page | Yes 	 | bool 			 | Whether the watermark should only be imprinted on the first page, otherwise all pages

### Example
```xml
<preprocessor name="watermark">
  <text>Hello world!</text>
  <opacity>0.2</opacity>
  <font-size>24</font-size>
  <only-first-page>false</only-first-page>
</preprocessor>
```

