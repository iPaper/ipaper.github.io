---
title: Return Codes
permalink: /backend-api/return-codes
redirect_from: "/display/DOC/Return+Codes"
tags: Flipbook Backend API
---

## CLIENT_ALREADY_HAD_MODULE

## CLIENT_INVALID_UNIT_COUNT

## CLIENT_UNKNOWN

## CUSTOMFIELD_FIELD_DOES_NOT_EXIST

## CUSTOMFIELD_FIELD_NAME_IS_NOT_UNIQUE

This code is returned if a custom field is added that does not have a unique name.

Solutions:
: Change the name
: Delete the existing field that uses the same name.

## CUSTOMFIELD_INVALID_DATA_FORMAT

This code is returned when a generic error occurs. Usually this signals an unexpected / unhandled error occured. Some API methods are more granular in their error responses than others, and thus a method might also return an ERROR for specific and/or more common errors.
An API method may begin returning more specific error codes at a later stage, but any non-success code will always indiciate an error condition.

## CUSTOMFIELD_INVALID_DATATYPE

## CUSTOMFIELD_INVALID_FIELD_NAME

## ERROR

## LICENSE_DOES_NOT_ALLOW_PROCESSING

This error is returned if the license of the iPaper does not allow further processing. The license will have to be upgraded to allow further processings.

## LOGIN_SECURITY_VIOLATION

## PAPER_DOES_NOT_EXIST

Returned whenever an iPaper ID is requested that does not exist.

## PAPER_MUST_NOT_BE_CATEGORY

## READONLY

During certain upgrade procedures, we will have to put the system in a read only mode. The frontend will be fully functional, as will all API read operations. Logins to the backend will be blocked, and API functions modifying data will return the READONLY status.

## RIPPER_CANNOT_PROCESS_PAPER_ALREADY_BEING_PROCESSED

A given iPaper can only be processed with one PDF at a time. This error is returned if an attempt is made to start a new process of an iPaper that is already being processed.

## RIPPER_INVALID_BASE64_PDF_FILE

This code is returned if:
: A PDF file was not provided.
: The provided base64 string could not be parsed / was invalid.

## SEARCH_CUSTOMFIELD_DATATYPE_DOES_NOT_SUPPORT_WILDCARDS

## SEARCH_NO_CUSTOM_FIELD_CRITERIAS

## SUCCESS
The SUCCESS return code indicates that the requested operation completed successfully.
Further information / requested data may be available in the messsage and data fields.
Any method that performs a request without errors & problems will always return a SUCCESS code.