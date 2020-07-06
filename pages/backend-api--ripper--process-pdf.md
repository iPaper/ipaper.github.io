---
title: Ripper.ProcessPDF
permalink: /backend-api/ripper/process-pdf
redirect_from: "/display/DOC/ProcessPdf"
tags: Flipbook Backend API
---

## Description

Begins a processing of a Flipbook.

## Parameters

| Name       | Value
|------------|---------------------------------------------
| paperID    | The ID of the Paper to process
| xmlOptions | Extra XML options for the processing request (See below)
| base64Pdf  | The PDF file encoded as a base64 string

### xmlOptions

| Name 								| Required 					 | Datatype | Default value 	 | Description
|-----------------------------------|----------------------------|----------|--------------------|------------------------------------------------------------------------------------------------------------------------------
| preserve-index 					| No 						 | bool 	| true 				 | Whether to preserve the current index of the Flipbook
| pages-from 						| When 'all-pages' = false   | int 		| 1 				 | The starting page in the catalog processing should begin from
| pages-to 							| When 'all-pages' = false   | int 		| [last page of pdf] | The ending page in the catalog processing should end with
| all-pages 						| No 						 | bool 	| true 				 | If true, pages-from and pages-to will be ignored, all pages will be processed. If false, pages-from and pages-to must be set
| preserve-links 					| No 						 | bool 	| true 				 | Whether to preserve current links on pages or clear them
| import-bookmarks 					| No 						 | bool 	| false 			 | Whether to import bookmarks from the PDF as index. Assumes preserve-index=false
| import-links-styleid 				| When 'import-links' = true | int 		| 					 | The linkstyle ID of style that imported links should assume
| password 							| No 						 | string 	| 					 | Password to unlock protected PDF. Will fail if PDF is protected and correct password is not provided
| preprocessors						| No 						 | XML 		| 					 | Preprocessors that needs to be run before the PDF is processed
| custom-link-import-configuration	| No 						 | string 	| 					 | The configuration XML for the custom link import to be executed. This should only be used if instructed to do so by iPaper
| enrichment-automation-name  | No  | string  |   | The name of the enrichment automation configuration that should be used when processing the PDF.

## Sample Response
```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></ code>
  <message><![CDATA[Process queued successfully.]]></message>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* RIPPER_CANNOT_PROCESS_PAPER_ALREADY_BEING_PROCESSED
* RIPPER_INVALID_BASE64_PDF_FILE
* LICENSE_DOES_NOT_ALLOW_PROCESSING