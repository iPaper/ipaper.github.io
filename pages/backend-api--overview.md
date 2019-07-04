---
title: Backend API Overview
permalink: /backend-api/overview
redirect_from: "/display/DOC/Backend+API"
---

## General Guidelines

* If an API returns a humanly read message, do not rely on it. It may change over time without notification. The message is only intended to help you understand the return code.
* Anything but a SUCCESS return code should be treated as an error. An ERROR return code may be changed with a more specific return code at a later stage, but a SUCCESS code will never be changed without previous notification.
* Any breaking changes will either be notified in due time, or a new API version will be setup so the old one can run concurrently.
* API methods may be appended without there being created a new overall API version, but only as long as they add non-breaking features like optional fields and extra return data. As a result of this, do use XPATH to query results, you should not rely on element index positions.

## API Endoint URL

The actual endpoint URL depends on which partner the solution is hosted at. For direct customers of iPaper, the endpoint is:

```
https://ipaper.api.ipapercms.dk
```

For other partners, the endpoint is:

```
https://<partner>.api.ipapercms.dk
```
