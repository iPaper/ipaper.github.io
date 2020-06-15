---
permalink: /integration/event-tracking-by-adobe-analytics
title: Event tracking using Adobe Analytics
summary: How event tracking works on your flipbook when you add Adobe Analytics integration.
---

## Adding Adobe Analytics integration

Adobe Analytics Integration can be enabled by copying the [launch embed code](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html) and pasting in into your flipbook integration settings.

## Events

All events are trackked according to the [launch object reference published by Adobe Analytics](https://docs.adobe.com/content/help/en/launch/using/reference/client-side-info/launch-object-reference.html).

```javascript
window._satellite.track(identifier, detail);
```

### Overview

<table>
	<thead>
		<tr>
			<th>Identifier</th>
			<th>Detail</th>
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

### Example

For example, when somebody searches for "Cute puppies" in your flipbook, we will track it as such via the "Search" event:

```javascript
window._satellite.track('Search', {
	'Term': 'Cute puppies'
});
```

## Page views
Pageviews are tracked as a separate event by its own:

```javascript
window._satellite.track('pageview', {
	page: [PAGE_URL],
	title: [PAGE_TITLE]
})
```