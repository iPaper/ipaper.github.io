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
> **NOTE:** All events are tracked to the **iPaper events** category

| Action | Label | Comment |
| ------ | ----- | ------- |
| External Link Click | HoverText: {linkHoverText} \| Url: {externalUrl} \| Page: {pageNumber} |
| PDF Download | n.a. | n.a. |
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
With Google Tag Manager you can track the initial Page views, any paging done in the flipbook, and actions performed in the flipbook.

> **NOTE:**  When using Google Tag Manager to track to Google Analytics, it's important that you haven't also defined an [Analytics Tracking ID](https://help.ipaper.io/article/127-integrate-google-analytics-with-ipaper), since this will result in pageviews and events getting tracking twice or more. If Google Tag Manager is not used to track to Google Analytics, it's okay to include both tags, but it's adviced to stick with one or the other to keep your tracking as simple as possible.

### Events
For all events we support, we'll push the raw event data and the Category, Action and Label that we'd push to Google Analytics for the similar event.

For the events below we will push to the data layer in the following format

```javascript
{
	'event': [EVENT_NAME],
	'ipaperEventParams': [EVENT_DATA],
	'ipaperEventCategory': [GOOGLE_ANALYTICS_EVENT_CATEGORY],
	'ipaperEventAction': [GOOGLE_ANALYTICS_EVENT_ACTION],
	'ipaperEventLabel': [GOOGLE_ANALYTICS_EVENT_LABEL]
}
```

#### Event overview

| Event name | Event data |
| -- | -- |
| ipaperEvent_externalLinkClick | `{ HoverText: string, Url: string, Page: number }` |
| ipaperEvent_popupImageClick | `{ HoverText: string, Url: string, Page: number }` |
| ipaperEvent_popupGalleryImageClick | `{ HoverText: string, Page: number }` |
| ipaperEvent_popupContentClick | `{ HoverText: string, Page: number }` |
| ipaperEvent_popupFrameClick | `{ HoverText: string, Url: string, Page: number }` |
| ipaperEvent_productAddedToCart | `{ ID: string; Name: string; Page: number }` |
| ipaperEvent_newsTickerExternalLinkClick | `{ HoverText: string, Url: string, Page: number }` |
| ipaperEvent_videoPlay | `{ Url: string, VideoType: string, Page: number }` |
| ipaperEvent_search | `{ Term: string }` |
| ipaperEvent_shopCheckout | `{ NumberOfProducts: number, CheckoutType: string, BasketValue: number; }` |
| ipaperEvent_leadgenPopupOpen | `{ Name: string, Url: string }` |
| ipaperEvent_leadgenPopupConversion | `{ Name: string, Url: string }` |
| ipaperEvent_leadgenPopupConversionByUrlClick | `{ Name: string, Url: string }` |

#### Example 
An example of a DataLayer push for the event `ipaperEvent_externalLinkClick` could look like this:
```javascript
window.dataLayer.push({
	'event': 'ipaperEvent_externalLinkClick',
	'ipaperEventParams': {
		HoverText: 'The clicked links hover text', 
		Url: 'http://ipaper.io/', 
		Page: 12
	},
	'ipaperEventCategory': 'iPaper events',
	'ipaperEventAction': 'External Link Click',
	'ipaperEventLabel': 'HoverText: The clicked links hover text | Url: http://ipaper.io/ | Page: 12'
})
```

### Extras
Aside from the DataLayers above we also push `PageElementClicked`, but it's only triggered for  the **internal** & **external** linktype.

| Event name         | Data | Comment |
| ------------------ | ---- | ------- |
| PageElementClicked | `{ type: 'internal' | 'external', data: { url: String, pagenumber: String } }`     | Triggered on **internal** & **external** linktype |

The following features have also been enabled for GTM:

```
['ua', 'ga', 'v', 'e', 'u', 'c', 'img', 'adm', 'awct', 'sp', 'gcs', 'ctv', 'f', 'smm', 'r', 'k', 'flc', 'fls' ]
```

You can find more information about what they entail on this page:
[https://developers.google.com/tag-manager/devguide](https://developers.google.com/tag-manager/devguide)
