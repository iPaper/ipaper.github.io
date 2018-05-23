---
permalink: /integration/events-tracked-by-google-analytics-and-tag-manager
title: Events tracked by Google Analytics / Tag Manager
---

## Google Analytics
We track **Pageviews** (both initial load and if enduser pages the flipbook) in Google Analytics.

Each page in an iPaper flipbook has a unique URL, and we push a pageview to GA like this:
```javascript
{ 'event': 'virtualPageview', 'virtualPageURL': flipbookurl + '?Page=' + pagenumber }
```

We'll also track various **Events** across our flipbooks. Take a look at the list below for a full list of events.
> NOTE: All events are tracked to the **iPaper events** category

| Action | Label | Comment |
| ------------- | ------------- | -- |
| External Link Click | HoverText: {linkHoverText} \| Url: {externalUrl} \| Page: {pageNumber} |
| Popup Image Click | HoverText: {linkHoverText} \| Url: {imageUrl} \| Page: {pageNumber} |
| Popup Image Gallery Click | HoverText: {linkHoverText} \| Page: {pageNumber} |
| Popup Content Click | HoverText: {linkHoverText} \| Page: {pageNumber} |
| Popup Frame Click | HoverText: {linkHoverText} \| Url: {frameUrl} \| Page: {pageNumber} |
| Product Added to Basket | Id: {productId} \| Name: {productName} \| Page: {pageNumber} |
| Newsticker External Link Click | Url: {externalUrl} |
| Video Play | Url: {videoUrl} \| VideoType: {'Video' / 'YouTube' / 'Vimeo'} \| Page: {pageNumber} | Only first **Play** on each page is tracked |
| Search | Term: {searchTerm} |
| Shop Checkout | NumberOfProducts: {numberOfProductsInCart} \| CheckoutType: {'Email' / 'ShareEmail' / 'Checkout' / 'Print'} \| BasketValue: {totalBasketValue} |

> NOTE: The values in `{}` will be replaced with context specific value before sending the event.

Here's how we'd send the **Search** event
```javascript
ga(tracker.get('name') + '.send', 'event', 'iPaper events', 'Search', 'Term: Cute puppies');
```

If you need help setting up Google Analytics on your iPaper account, have a look at our [Integrate Google Analytics With iPaper
Google Analytics Tracking](https://help.ipaper.io/article/127-integrate-google-analytics-with-ipaper) guide.

## Google Tag Manager
We track **PageElementClicked** for linktypes **internal** & **external**.

The following features have also been enabled for GTM:

```
['ua', 'ga', 'v', 'e', 'u', 'c', 'img', 'adm', 'awct', 'sp', 'gcs', 'ctv', 'f', 'smm', 'r', 'k', 'flc', 'fls' ]
```

You can find more information about what they entail on this page:
[https://developers.google.com/tag-manager/devguide](https://developers.google.com/tag-manager/devguide)
