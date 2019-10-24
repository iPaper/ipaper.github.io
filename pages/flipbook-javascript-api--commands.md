---
permalink: /flipbook-javascript-api/commands
title: Commands
summary: Commands are instructions issued by the parent window to the iframed flipbook. Commands can be invoked by calling magic methods, which can be accessed directly from the API instance.
---

## Overview

<img src="/images/flipbook-javascript-api/commands.svg" style="max-width: 100%; max-height: 100%" />

Commands are issued from the parent window (your website) to the JavaScript API. The API then relays the command via `window.postMessage()` to the iframed flipbook.

## Flipbook-related commands

### `updateEventSettings`

It is possible to dictate how the iframed flipbook should handle events when they have been triggered. The method accepts a single argument that is an object containing the following keys, which references events that the v2 Flipbook API listens to:

- [`onBasketClick`](./events#onbasketclick)
- [`onItemAdd`](./events#onitemadd)
- [`onPageElementClick`](./events#onpageelementclick)

The keys should contain an object of the following format: `{ preventDefault: <boolean> }`, where `<boolean>` is `true` or `false`. When `preventDefault` is set to `true`, the flipbook will perform the default action associated with each event. If set to `false`, the default action will be skipped.

| Event                                               | Default action taking place in the flipbook                                                                        |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [`onBasketClick`](./events#onbasketclick)           | Opens the shop basket                                                                                              |
| [`onItemAdd`](./events#onitemadd)                   | Adds the item to the shop basket.<br />Triggered by any enrichment that adds a shop item (e.g. shop variant menu). |
| [`onPageElementClick`](./events#onpageelementclick) | Adds the item to the shop basket.<br />Triggered by clicking on an enrichment with shop item action.               |

An example use:

```js
// Disable opening of shop basket AND page element click on shop items
iPaperAPI.updateEventSettings({
	onBasketClick: { preventDefault: true },
	onPageElementClick: { preventDefault: true }
});
```


## Publication-related commands

### `goToPage`

Navigate to a specific page: the page number is to be provided as the one and only argument of the function. For example:

```js
iPaperAPI.goToPage(4);
```

### `goToPreviousPage`

Go to the previous spread (if flipbook has a spread-based layout), or the previous page (if flipbook has a page-based layout). This method accepts no arguments:

```
iPaperAPI.goToPreviousPage();
```

### `goToNextPage`

Go to the next spread (if flipbook has a spread-based layout), or the next page (if flipbook has a page-based layout). This method accepts no arguments:

```
iPaperAPI.goToNextPage();
```

## Shop-related commands

### `addItem`

Programmatically adds a custom item to the basket. This method accepts a single argument, consisting of properties of the shop item entity.

| Property      | Type     | Description                                |
| ------------- | -------- | ------------------------------------------ |
| `title`       | `string` | Shop item title                            |
| `description` | `string` | Shop item description                      |
| `productID`   | `string` | Shop item product ID                       |
| `originPage`  | `number` | Page number where the shop item is located |
| `price`       | `number` | Shop item price                            |
| `quantity`    | `number` | Number of items added                      |

Example use:

```js
iPaperAPI.addItem({
    title: 'My product',
    description: 'Product description',
    productID: 'PROD-25B',
    price: '29.95',
    originPage: 6,
    quantity: 1
});
```

## Advanced use

If you are accustomed to the `.trigger()` regime (such as that implemented in JQuery), you can also use it as such:

```js
iPaperAPI.trigger('goToPage', 4);
```

Refer to [**Event listeners and command triggers**](./advanced-usage#event-listeners-and-command-triggers) on the advanced usage page for a wholesome example.