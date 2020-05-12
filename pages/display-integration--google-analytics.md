---
permalink: /display-integration/google-analytics
title: Google Analytics
summary: Learn how to implement Google Analytics tracking in your Display
---

## Overview

Google Analytics tracking is configurable on a license-level: the same Google Analytics Tracking ID will be applied to all your Display instances in the same license, once configured.

## Events

All events are tracked to the **iPaper Display events** category in the following format:

<table>
	<thead>
		<tr>
			<th>Event name</th>
			<th>Interactive&nbsp;<sup><a href="#interactive-flag">1</a></sup></th>
			<th>Data&nbsp;<sup><a href="#event-labels">2</a></sup></th>
			<th>Comments</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Load</td>
			<td>No</td>
			<td><pre><code>{
  Url: [DISPLAY_URL]
}</code></pre></td>
			<td>&ndash;</td>
		</tr>
		<tr>
			<td>Time Spent</td>
			<td>No</td>
			<td><pre><code>{
  Duration: [DURATION_IN_SECONDS]
}</code></pre></td>
			<td>&ndash;</td>
		</tr>
		<tr>
			<td>Button Click</td>
			<td>Yes</td>
			<td><pre><code>{
  Url: [BUTTON_ENTITY_ACTION_URL]
}</code></pre></td>
			<td>&ndash;</td>
		</tr>
		<tr>
			<td>Image Click</td>
			<td>Yes</td>
			<td><pre><code>{
  Url: [IMAGE_ENTITY_ACTION_URL]
}</code></pre></td>
			<td>&ndash;</td>
		</tr>
		<tr>
			<td>Product Click</td>
			<td>Yes</td>
			<td><pre><code>{
  Id: [PRODUCT_ENTITY_PRODUCT_ID],
  Url: [PRODUCT_ENTITY_PRODUCT_URL]
}</code></pre></td>
			<td>&ndash;</td>
		</tr>
		<tr>
			<td>Video Click</td>
			<td>Yes</td>
			<td><pre><code>{
  Url: [VIDEO_ENTITY_ASSET_URL]
}</code></pre></td>
			<td>Only available for autoplaying video</td>
		</tr>
		<tr>
			<td>Video Start</td>
			<td>Yes</td>
			<td><pre><code>{
  Url: [VIDEO_ENTITY_ASSET_URL]
}</code></pre></td>
			<td>Only available for non-autoplaying video. Fires once per video entity, when a user manually plays video.</td>
		</tr>
		<tr>
			<td>Video Played 25 Percent</td>
			<td>Yes</td>
			<td><pre><code>{
  Url: [VIDEO_ENTITY_ASSET_URL]
}</code></pre></td>
			<td rowspan="4">Only available for non-autoplaying video. Fires once per video entity, once the timestamp of a video exceeds the stated percentage of its total duration.</td>
		</tr>
		<tr>
			<td>Video Played 50 Percent</td>
			<td>Yes</td>
			<td><pre><code>{
  Url: [VIDEO_ENTITY_ASSET_URL]
}</code></pre></td>
		</tr>
		<tr>
			<td>Video Played 75 Percent</td>
			<td>Yes</td>
			<td><pre><code>{
  Url: [VIDEO_ENTITY_ASSET_URL]
}</code></pre></td>
		</tr>
		<tr>
			<td>Video Played 100 Percent</td>
			<td>Yes</td>
			<td><pre><code>{
  Url: [VIDEO_ENTITY_ASSET_URL]
}</code></pre></td>
		</tr>
	</tbody>
</table>

### Interactive flag

There are some events that we want to mark as non-interactive (or ["non-interaction events"](https://developers.google.com/analytics/devguides/collection/analyticsjs/events?hl=da#non-interaction_events) by Google Analytics' definition). This will mean that even if these events are fired, the session will be considered as bounced if the user does not further interact with the page.

### Event labels

The data format below is represented in JSON. It is converted to a string for the `eventLabel` object using the following convention:

* Key names are PascalCased
* Key-value pairs are separated by the pipe character `|`

Example:

```javascript
{
  Id: [PRODUCT_ENTITY_PRODUCT_ID],
  Url: [PRODUCT_ENTITY_PRODUCT_URL]
}
```

&hellip;is converted into:

`Id: [PRODUCT_ENTITY_PRODUCT_ID] | Url: [PRODUCT_ENTITY_PRODUCT_URL] `