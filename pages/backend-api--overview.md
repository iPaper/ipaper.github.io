---
title: Backend API Overview
permalink: /backend-api/overview
redirect_from: "/display/DOC/Backend+API"
tags: Flipbook Backend API
---

## API reference

Our API uses resource-oriented URLs, accepts [form-encoded request](https://en.wikipedia.org/wiki/POST_(HTTP)#Use_for_submitting_web_forms) bodies, returns [XML](https://en.wikipedia.org/wiki/XML) responses, and authentication.

Our API provides an easy way for you to integrate with the iPaper Flipbook product from your backend.

You can use the API to access the most common actions also available from our CMS, which allows you to build your own software that leverages the iPaper product.

## General Guidelines

* If an API returns a humanly read message, do not rely on it. It may change over time without notification. The message is only intended to help you understand the return code.
* Anything but a SUCCESS return code should be treated as an error. An ERROR return code may be changed with a more specific return code at a later stage, but a SUCCESS code will never be changed without previous notification.
* Any breaking changes will either be notified in due time, or a new API version will be setup so the old one can run concurrently.
* API methods may be appended without there being created a new overall API version, but only as long as they add non-breaking features like optional fields and extra return data. As a result of this, do use XPATH to query results, you should not rely on element index positions.

## Best practice

* **Keep your credentials safe**  
While our endpoint allows for you to use GET requests, we strongly suggest you use POST.
Using GET requests will send any credentials as clear text over the internet even if sent via HTTPS.

* **Rate limit your requests**  
You should keep requests to our API below **50 per minute**.  
Some requests like for instance `Paper.GetAllPapers` will return the same result every time unless someone/something has made changes since the last request, so consider adding a short lived cache on your end, or only make calls when you know there there are changes.

* **Use caching where possible**  
Depending on the endpoint you call in the API, you should cache responses when possible.  
Caching results that aren't prone to changes will make your software faster since you save a roundtrip to our API for data you already have.

* **Use the proper abstractions**  
If you have a website or app that uses data from iPaper, you should create an endpoint in your backend that your services talk to.
Having your own endpoint allows you to manage caching, hide credentials, transform API results and much more.  
Don't call our API directly from any code that runs on user devices, e.g. apps, websites, etc. as this introduces the risk of end-users grabbing the credentials and misusing them.

## API Endoint URL

The actual endpoint URL depends on which partner the solution is hosted at. For direct customers of iPaper, the endpoint is:

```
https://ipaper.api.ipapercms.dk
```

For other partners, the endpoint is:

```
https://<partner>.api.ipapercms.dk
```

