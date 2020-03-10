---
permalink: /integration/events-tracked-by-google-analytics-and-tag-manager
title: Events tracked by Google Analytics / Tag Manager
---

## Google Analytics
We track **Pageviews** (both initial load and if end user pages the flipbook) in Google Analytics. On top of that, we also track various **Events** across our flipbooks. Take a look at the list below for a full list of events.

### Events

All events are tracked to the **iPaper events** category in the following format:

```javascript
window.ga(tracker.get('name') + '.send', {
	hitType: 'event',
	eventCategory: 'iPaper events',
	eventAction: [ACTION],
	eventLabel: [LABEL]
});
```

#### Overview

| Action | Label | Comment |
| ------ | ----- | ------- |
| External Link Click | HoverText: {linkHoverText} \| Url: {externalUrl} \| Page: {pageNumber} | n.a. |
| Load | Url: {flipbookUrl} | Flipbook URL is simply read from `window.location.href` |
| Page Element Click | [See more info below](#page-element-click-tracking-on-ga-and-gtm) | n.a. |
| PDF Download | n.a. | n.a. |
| Popup Image Click | HoverText: {linkHoverText} \| Url: {imageUrl} \| Page: {pageNumber} | n.a. |
| Popup Image Gallery Click | HoverText: {linkHoverText} \| Page: {pageNumber} | n.a. |
| Popup Content Click | HoverText: {linkHoverText} \| Page: {pageNumber} | n.a. |
| Popup Frame Click | HoverText: {linkHoverText} \| Url: {frameUrl} \| Page: {pageNumber} | n.a. |
| Product Added to Basket | Id: {productId} \| Name: {productName} \| Page: {pageNumber} | n.a. |
| Newsticker External Link Click | Url: {externalUrl} | n.a. |
| Video Play | Url: {videoUrl} \| VideoType: {'Video' / 'YouTube' / 'Vimeo'} \| Page: {pageNumber} | Only first **Play** on each page is tracked |
| Search | Term: {searchTerm} | n.a. |
| Shop Checkout | NumberOfProducts: {numberOfProductsInCart} \| CheckoutType: {'Email' / 'ShareEmail' / 'Checkout' / 'Print'} \| BasketValue: {totalBasketValue} | n.a. |

{% include note.html content="The values in `{}` will be replaced with context specific value before sending the event." %}

#### Example

For example, when somebody searches for "Cute puppies" in your flipbook, we will track it as such via the "Search" event:

```javascript
window.ga(tracker.get('name') + '.send', {
	hitType: 'event',
	eventCategory: 'iPaper events',
	eventAction: 'Search',
	eventLabel: 'Term: Cute puppies'
});
```

If you need help setting up Google Analytics on your iPaper account, have a look at our [Integrate Google Analytics With iPaper
Google Analytics Tracking](https://help.ipaper.io/en/articles/1857330-google-analytics-part-one-how-to-integrate-and-the-benefits-of-using-ga-with-ipaper) guide.

## Google Tag Manager
Similar to Google Analytics, we track **Pageviews** (both initial load and if end user pages the flipbook) in Google Tag Manager. Pageviews on GTM are tracked as such:

```javascript
window.dataLayer.push({
	event: 'virtualPageview',
	virtualPageUrl: [FLIPBOOK_PAGE_URL],
	virtualPageTitle: [FLIPBOOK_PAGE_TITLE],
});
```

On top of that, we also track various **Events** across our flipbooks.

{% include note.html content="When using Google Tag Manager to track to Google Analytics, it's important that you haven't also defined an [Analytics Tracking ID](https://help.ipaper.io/en/articles/1857330-google-analytics-part-one-how-to-integrate-and-the-benefits-of-using-ga-with-ipaper), since this will result in pageviews and events getting tracking twice or more. If Google Tag Manager is not used to track to Google Analytics, it's okay to include both tags, but it's adviced to stick with one or the other to keep your tracking as simple as possible." %}

### Events
For all events we support, we'll push the raw event data and the Category, Action and Label that we'd push to Google Analytics for the similar event.

For the events below we will push to the data layer in the following format

```javascript
window.dataLayer.push({
	'event': [EVENT_NAME],
	'ipaperEventParams': [EVENT_DATA],
	'ipaperEventCategory': [GOOGLE_ANALYTICS_EVENT_CATEGORY],
	'ipaperEventAction': [GOOGLE_ANALYTICS_EVENT_ACTION],
	'ipaperEventLabel': [GOOGLE_ANALYTICS_EVENT_LABEL]
});
```

#### Overview

<div class="table-wrapper" markdown="block">

| Event name | Event data |
| -- | -- |
| ipaperEvent_externalLinkClick | `{ HoverText: string, Url: string, Page: number }` |
| ipaperEvent_load | `{ Url: string }` |
| ipaperEvent_pageElementClick | [See more info below](#page-element-click-tracking-on-ga-and-gtm) |
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
| ipaperEvent_leadgenPopupConversionByUrlClick | `{ Name: string, Url: string }` |'

</div>

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

The following features have also been enabled for GTM:

```
['ua', 'ga', 'v', 'e', 'u', 'c', 'img', 'adm', 'awct', 'sp', 'gcs', 'ctv', 'f', 'smm', 'r', 'k', 'flc', 'fls' ]
```

## Page element click tracking on GA and GTM

Aside from the events listed above for GA and GTM, we also track the `PageElementClicked` event, but it's only triggered for the **internal** & **external** linktype.

<table>
	<thead>
		<tr>
			<th>Event name</th>
			<th>Data</th>
			<th>Comment</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>PageElementClicked</td>
			<td><pre><code>{
  Type: 'internal' | 'external',
  Data: {
    Url: String,
    Pagenumber: String
  }
}</code></pre></td>
			<td>Triggered on <strong>internal</strong> and <strong>external</strong> linktypes <em>only</em></td>
		</tr>
	</tbody>
</table>

You can find more information about what they entail on this page:
[https://developers.google.com/tag-manager/devguide](https://developers.google.com/tag-manager/devguide)
