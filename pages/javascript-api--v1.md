---
permalink: /javascript-api/v1
title: Legacy JavaScript API (v1)
redirect_from: "/display/DOC/JavaScript+API"
summary: The JavaScript API allows you listen for events occurings in the Flipbook, prevent default actions and invoking functions in the Flipbook.
---

## Requirements

* A working Branded Domain module. Specifically, the actual Flipbook needs to be on a subdomain to the domain on which the iframe is placed.

## Embedding the Flipbook

Before gaining access to the API, you'll have to embed it on your own website. Technically the embedding works by iframing the Flipbook onto your own website.
For JavaScript to work across domains, the Flipbook must be hosted on a subdomain to the domain where it's embedded into. Thus, if your website is ```www.frontend.dk```, the Flipbook will have to be setup on a custom hostname like catalogs.frontend.dk. Internally, iPaper sets the page domain to the top domain. Thus, while the Flipbook is hosted at catalogs.frontend.dk, it will set its domain to frontend.dk. For the scripts to be able to work cross-domain, you must set the domain on your own website as well, even if it's hosted on frontend.dk already. Include the following snippet to set the domain:

```html
<script type="text/javascript">
    document.domain = "frontend.dk";
</script>
```

## Initialization

Once the Flipbook API has been loaded and initialized in the Flipbook, it will attempt to call an iPaperInit method in the parent window. As a parameter, a reference to the API is passed. Using this reference, you can hook up any events you wish to listen for, as well as keep a reference to the API for later interaction.

The following is a complete example of a host page running on frontend.dk, with the catalog being loaded from a subdomain. We're hooking up to the Shops "addItem" event, being fired once an item is about to be added to the basket.

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <title>iPaper JS Integration Test</title>
        <script type="text/javascript">
            document.domain = 'frontend.dk';

            function iPaperInit(api) {
                api.Shop.addEventListener("addItem", function(data) {
                    alert("Item added: " + data.title);
                });
            }
        </script>
    </head>
    <body>

        <iframe src="http://flex.frontend.dk/Mark/VeksHovedkatalog/" style="width: 100%; height: 300px"></iframe>

    </body>
</html>
```

## Listening for Events

All event dispatchers support the addEventListener method, taking in two parameters. The first parameter is the event name to listen for, as documented on the specific event dispatchers pages. The second parameter is a callback method that will be called when the event fires, including a potential data parameter if the event includes data. This parameter will be null in cases where the event does not include data.
Sample:

```javascript
function iPaperInit(api) {
    api.Shop.addEventListener("addItem", function(data) {
        alert("Item added: " + data.title);
    });
}
```

## Responding to Events

Some events accept a response object, changing the behavior of the Flipbook. As an example, the Shop addItem event allows you to prevent the default action of adding the item to the Flipbook shop basket. To do so, see this example:

```javascript
function iPaperInit(api) {
    api.Shop.addEventListener("addItem", function(data) {
        // Do something with the added item

        return {
            preventDefault: true
        }
    });
}
```
{% include important.html content="If multiple event listeners are added, their responses will be concatenated. Thus, if multiple event listeners return a value for the preventDefault attribute, the last event listeners value will be returned, while the others will be ignored." %}

## Calling Method
Some event dispatchers supports a number of functions that can be called through JavaScript. One example is the addItem method on the Shop event dispatcher, used for programmatically adding items to the basket through JavaScript. Sample:

```javascript
api.Shop.addItem({
    title: 'Product title',
    description: 'Product description',
    price: 29.95,
    productID: 'Product ID'
});
```

## Event Dispatchers
The API has a number of event dispatchers, each used for dispatching and listening to events within a certain area/module of the iPaper. The event dispatchers may also have methods for interacting with the iPaper itself as well.

### Publication event dispatcher

The publication event dispatcher contains methods for listening to and interacting with the publication in Flipbooks.

#### Events
These are events that you can listen for using the addEventListener() method on the event dispatcher.

##### onPageElementClicked

Fired when a pageelement is "clicked".
{% include note.html content="Current only shopitems will fire this event!" %}

| Property | Type | Description |
| -------- | ---- | ----------- |
| `type`  | `string` | The page element type that was clicked on |
| `data` | `{}` | Data associated with the page element |
| `event` | `{}` | Event data associated with the click event |
| `event.originPage` | `number` | Page number on which the page element is located on |
| `event.originSpreadPages` | `number[]` | Page numbers on which the spread where the page element is located on |
| `event.coordinates.pageX` | `number` | Absolute x coordinate of the click event |
| `event.coordinates.pageY` | `number` | Absolute y coordinate of the click event |
| `event.bookX` | `number` | Ratio of the x coordinate relative to book width |
| `event.bookY` | `number` | Ratio of the y coordinate relative to book height |

**Sample data**:

```javascript
{
    type: 'shopitem',
    data: {
        title: 'Coca Cola',
        description: 'Carbonated soft drink ',
        productID: 'C1',
        price: 9.95,
        amountselection: true|false,
        packagesize: 1
    },
    event: {
        originPage: 4,
        originSpreadPages: [4,5],
        coordinates: {
            pageX: 525,
            pageY: 250,
            bookX: 0.523234,
            bookY: 0.124543
        }
    }
}
```

**Return values**:

```javascript
{
    preventDefault: true // If set to true, the item will not be added to the Flipbook basket.
}
```

##### onSpreadChanged
Fired whenever a paging event is registered by the Flipbook.

| Property              | Type       | Description |
| --------------------- | ---------- | ----------- |
| `currentSpreadPages`  | `number[]` | Page numbers that are in the current spread |
| `currentVisiblePages` | `number[]` | Page number(s) that are currently in view. This array may contain one or two numbers, depending if the current view is page- (mobile/tablet in portrait) or spread-based (desktop, or mobile/tablet in landscape). | 

**Sample data:**

```javascript
{
    currentSpreadPages: [4,5],
    currentVisiblePages: [4,5]
}
```

#### Methods
These are methods that you can call on the event dispatcher.

##### gotoPage

Navigates to the specified page.

**Sample:**

```javascript
api.Publication.gotoPage(5);
```

### Shop event dispatcher

The shop event dispatchers contains methods for listening to and interacting with the shop module in Flipbook.

#### Events
These are events that you can listen for using the addEventListener() method on the event dispatcher.

##### addItem

Fired when a shop item is added to the basket.

**Sample data**:

```javascript
{
    title: 'My product',
    description: 'Product description',
    productID: 'PROD-25B',
    price: '29.95',
    originPage: 6
}
```

**Return values**:

```javascript
{
    preventDefault: true // If set to true, the item will not be added to the Flipbook basket.
}
```

##### onBasketClick
Fired when the open basket icon is clicked in the Flipbook.

**Return values:**

```javascript
{
    preventDefault: true // If set to true, the basket will not be opened.
}
```

#### Methods
These are methods that you can call on the event dispatcher.

##### addItem

Adds an item to the Flipbook basket.

**Sample:**

```javascript
api.Shop.addItem({
    title: 'My product',
    description: 'Product description',
    productID: 'PROD-25B',
    price: '29.95',
    originPage: 6,
    quantity: 1
});
```