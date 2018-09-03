---
permalink: /javascript-api/publication
title: Publication (Event Dispatcher)
redirect_from: "/display/DOC/Publication"
---

The publication event dispatcher contains methods for listening to and interacting with the publication in Flipbooks.

## Events
These are events that you can listen for using the addEventListener() method on the event dispatcher.

### onPageElementClicked

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

### onSpreadChanged
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

## Methods
These are methods that you can call on the event dispatcher.

### gotoPage

Navigates to the specified page.

**Sample:**

```javascript
api.Publication.gotoPage(5);
```
