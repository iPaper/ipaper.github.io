---
permalink: /integration/events-tracked-by-google-analytics-and-tag-manager
title: Events tracked by Google Analytics / Tag Manager
tags: Flipbook integration
summary: How event tracking works on your flipbook when you add Google Analytics or Google Tag Manager integration.
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

<table class="table-fixed table-condensed">
	<thead>
		<tr>
			<th>Event name</th>
			<th>Data <a href="#event-labels-in-ga-and-gtm">(conversion to eventLabel)</a></th>
			<th>Comment</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>External Link Click</td>
			<td><pre><code>{
  HoverText: [LINK_HOVER_TEXT],
  Url: [EXTERNAL_URL],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>Load</td>
			<td><pre><code>{
  Url: [FLIPBOOK_URL]
}</code></pre></td>
			<td>Flipbook URL is simply read from <code>window.location.href</code></td>
		</tr>
		<tr>
			<td>PDF Download</td>
			<td>n.a.</td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>Popup Image Click</td>
			<td><pre><code>{
  HoverText: [LINK_HOVER_TEXT],
  Url: [IMAGE_URL],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>Popup Image Gallery Click</td>
			<td><pre><code>{
  HoverText: [LINK_HOVER_TEXT],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>Popup Content Click</td>
			<td><pre><code>{
  HoverText: [LINK_HOVER_TEXT],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>Popup Frame Click</td>
			<td><pre><code>{
  HoverText: [LINK_HOVER_TEXT],
  Url: [FRAME_URL],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>Product Added to Basket</td>
			<td><pre><code>{
  Id: [PRODUCT_ID],
  Name: [PRODUCT_NAME],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>Newsticker External Link Click</td>
			<td><pre><code>{
  Url: [EXTERNAL_URL]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>Search</td>
			<td><pre><code>{
  Term: [SEARCH_TERM]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>Shop Checkout</td>
			<td><pre><code>{
  NumberOfProducts: [NO_OF_PRODUCT_IN_CART],
  CheckoutType: [CHECKOUT_TYPE],
  BasketValue: [TOTAL_BASKET_VALUE]
}</code></pre></td>
			<td>Possible <code>CheckoutType</code> values are <code>Email</code>, <code>ShareEmail</code>, <code>Checkout</code>, or <code>Print</code>.</td>
		</tr>
		<tr>
			<td>Video Play</td>
			<td><pre><code>{
  Url: [VIDEO_URL],
  VideoType: [VIDEO_TYPE],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td><strong>Only the first play is registered.</strong> Possible <code>VideoType</code> values are <code>Video</code>, <code>YouTube</code>, or <code>Vimeo</code>.</td>
		</tr>
	</tbody>
</table>

{% include note.html content="The values in `[]` will be replaced with context specific value before sending the event." %}

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

<table class="table-fixed table-condensed">
	<thead>
		<tr>
			<th scope="col">Event name</th>
			<th scope="col">Data <a href="#event-labels-in-ga-and-gtm">(conversion to eventLabel)</a></th>
			<th scope="col">Comment</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>ipaperEvent_<wbr />externalLinkClick</td>
			<td><pre><code>{
  HoverText: [LINK_HOVER_TEXT],
  Url: [EXTERNAL_URL],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />load</td>
			<td><pre><code>{
  Url: [FLIPBOOK_URL]
}</code></pre></td>
			<td>Flipbook URL is simply read from <code>window.location.href</code></td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />PDFDownload</td>
			<td>n.a.</td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />leadgenPopupOpen</td>
			<td><pre><code>{
  Name: [POPUP_NAME],
  Url: [CURRENT_URL]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />leadgenPopupConversion</td>
			<td><pre><code>{
  Name: [POPUP_NAME],
  Url: [CURRENT_URL]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />leadgenPopupConversionByUrlClick</td>
			<td><pre><code>{
  Name: [POPUP_NAME],
  Url: [CURRENT_URL]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />popupImageClick</td>
			<td><pre><code>{
  HoverText: [LINK_HOVER_TEXT],
  Url: [IMAGE_URL],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />popupGalleryImageClick</td>
			<td><pre><code>{
  HoverText: [LINK_HOVER_TEXT],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />popupContentClick</td>
			<td><pre><code>{
  HoverText: [LINK_HOVER_TEXT],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />popupFrameClick</td>
			<td><pre><code>{
  HoverText: [LINK_HOVER_TEXT],
  Url: [FRAME_URL],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />productAddedToCart</td>
			<td><pre><code>{
  Id: [PRODUCT_ID],
  Name: [PRODUCT_NAME],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />newsTickerExternalLinkClick</td>
			<td><pre><code>{
  Url: [EXTERNAL_URL]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />search</td>
			<td><pre><code>{
  Term: [SEARCH_TERM]
}</code></pre></td>
			<td>n.a.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />shopCheckout</td>
			<td><pre><code>{
  NumberOfProducts: [NO_OF_PRODUCT_IN_CART],
  CheckoutType: [CHECKOUT_TYPE],
  BasketValue: [TOTAL_BASKET_VALUE]
}</code></pre></td>
			<td>Possible <code>CheckoutType</code> values are <code>Email</code>, <code>ShareEmail</code>, <code>Checkout</code>, or <code>Print</code>.</td>
		</tr>
		<tr>
			<td>ipaperEvent_<wbr />videoPlay</td>
			<td><pre><code>{
  Url: [VIDEO_URL],
  VideoType: [VIDEO_TYPE],
  Page: [PAGE_NUMBER]
}</code></pre></td>
			<td><strong>Only the first play is registered.</strong> Possible <code>VideoType</code> values are <code>Video</code>, <code>YouTube</code>, or <code>Vimeo</code>.</td>
		</tr>
	</tbody>
</table>

#### Example 
An example of a DataLayer push for the event `ipaperEvent_<wbr />externalLinkClick` could look like this:
```javascript
window.dataLayer.push({
	'event': 'ipaperEvent_<wbr />externalLinkClick',
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

## Page element click tracking on GTM

Aside from the events listed above, we also track the `PageElementClicked` event, but it's only triggered for the **internal** & **external** linktype.

<table class="table-fixed table-condensed">
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

## Event labels in GA and GTM

The data format below is represented in JSON. It is converted to a string for the `eventLabel` object using the following convention:

* Key names are PascalCased
* Key-value pairs are separated by the pipe character `|`

Example:

```javascript
{
  HoverText: [LINK_HOVER_TEXT],
  Url: [EXTERNAL_URL],
  Page: [PAGE_NUMBER]
}
```

&hellip;is converted into:

`HoverText: [LINK_HOVER_TEXT] | Url: [EXTERNAL_URL] | Page: [PAGE_NUMBER]`
