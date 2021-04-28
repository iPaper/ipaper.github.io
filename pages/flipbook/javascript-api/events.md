---
title: Events
permalink: /flipbook/javascript-api/events
redirect_from: /flipbook-javascript-api/events
summary: Events happen in the iframed flipbook and are emitted to the parent window. Our API catches these emitted events and invoke magic callbacks, which can be used to execute business-specific logic in the parent window, in response to specific events that have occurred in the iframed flipbook.
tags: Flipbook JS API
---

## Overview

<img src="/images/flipbook-javascript-api/events.svg" style="max-width: 100%; max-height: 100%" />

Events are dispatched from the iframed flipbook to the Javascript API via `window.postMessage()`. Once the API receives this event, it then invokes a callback present in the parent window.

## Publication-related events

### `onPageElementClick`

Fired when an enrichment/link with a shop item action is clicked.

{% include note.html content="Current only shop items will fire this event. Click events on any other enrichments are not emitted." %}

| Property                  | Type       | Description                                                                |
| ------------------------- | ---------- | -------------------------------------------------------------------------- |
| `type`                    | `string`   | The page element type that was clicked on                                  |
| `data`                    | `{}`       | Data associated with the page element                                      |
| `data.title`              | `string`   | Shop item title                                                            |
| `data.description`        | `string`   | Shop item description                                                      |
| `data.productId`          | `string`   | Shop item product ID                                                       |
| `data.price`              | `number`   | Shop item price                                                            |
| `data.amountSelection`    | `boolean`  | If users are allowed to manually specify an amount before adding to basket |
| `data.packageSize`        | `number`   | Number of items per package                                                |
| `event`                   | `{}`       | Event data associated with the click event                                 |
| `event.originPage`        | `number`   | Page number on which the page element is located on                        |
| `event.originSpreadPages` | `number[]` | Page numbers on which the spread where the page element is located on      |
| `event.coordinates.pageX` | `number`   | Absolute x coordinate of the click event                                   |
| `event.coordinates.pageY` | `number`   | Absolute y coordinate of the click event                                   |
| `event.bookX`             | `number`   | Ratio of the x coordinate relative to book width                           |
| `event.bookY`             | `number`   | Ratio of the y coordinate relative to book height                          |

### `onSpreadChange`

Fired when a paging event is registered in the flipbook.

| Property              | Type       | Description |
| --------------------- | ---------- | ----------- |
| `currentSpreadPages`  | `number[]` | Page numbers that are in the current spread |
| `currentVisiblePages` | `number[]` | Page number(s) that are currently in view. This array may contain one or two numbers, depending if the current view is page- (mobile/tablet in portrait) or spread-based (desktop, or mobile/tablet in landscape). | 

## Shop-related events

### `onBasketClick`

Fired when the basket icon is clicked to reveal the basket in the sidebar. There is no data returned by this event.

### `onItemAdd`

Fired when a shop item has been added to the basket.

| Property      | Type     | Description                                |
| ------------- | -------- | ------------------------------------------ |
| `title`       | `string` | Shop item title                            |
| `description` | `string` | Shop item description                      |
| `productId`   | `string` | Shop item product ID                       |
| `price`       | `number` | Shop item price                            |
| `originPage`  | `number` | Page number where the shop item is located |
| `quantity`    | `number` | Number of items added                      |
| `packageSize` | `number` | Number of items per package                |

## Advanced use

If you are accustomed to listening to events instead, that is possible with this API: simply bind the event listener to the iframe element:

```html
<iframe src="https://demo.ipaper.io" id="ipaper-flipbook">
```

The two options presented below are functionally identical.

```js
// Basic option: Using magic callbacks to listen to events
iPaperAPI.onSpreadChange = function(data) {
    console.log(data);
};

// Advanced option: Listening to events in the DOM
document.getElementById('ipaper-flipbook').addEventListener('onSpreadChange', function(data) {
    console.log(data);
});
```

Refer to [**Event listeners and command triggers**](./advanced-usage#event-listeners-and-command-triggers) on the advanced usage page for a wholesome example.