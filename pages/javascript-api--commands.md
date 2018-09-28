---
permalink: /javascript-api/commands
title: Commands
summary: Commands are instructions issued by the parent window to the iframed flipbook. Commands can be invoked by calling magic methods, which can be accessed directly from the API instance.
---

## Overview

<img src="/images/javascript-api/commands.svg" style="max-width: 100%; max-height: 100%" />

Commands are issued from the parent window (your website) to the JavaScript API. The API then relays the command via `window.postMessage()` to the iframed flipbook.

## Publication commands

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

## Shop commands

### `addItem`

Programmatically adds a custom item to the basket. This method accepts a single argument, consisting of properties of the shop item entity.

| Property      | Type     | Description                                |
|===============|==========|============================================|
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