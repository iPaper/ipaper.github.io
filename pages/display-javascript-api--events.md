---
permalink: /display-javascript-api/events
title: Events
summary: Display JavaScript API emits custom events that can be listened to on the document root
---

## Overview

The Display JavaScript API emits custom events to the document root so that you can keep track of changes to the Display API instance.

### `iPaperDisplayApiReady`

This event is emitted when the Display JavaScript API has successfully instantiated and populates the global scope with the `iPaperDisplayApi` object. At this point of time, all magic commands for the Display JavaScript API is accessible.

```js
document.addEventListener('iPaperDisplayApiReady', function () {
    // At the point in time, window.iPaperDisplayApi is available in the global scope
    window.iPaperDisplayApi.show();
});
```