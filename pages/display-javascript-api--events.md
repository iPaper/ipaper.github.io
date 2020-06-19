---
permalink: /display-javascript-api/events
title: Events
summary: Display JavaScript API emits custom events that can be listened to on the document root
tags: Display JS API
---

## Overview

The Display JavaScript API emits custom events to the document root so that you can keep track of changes to the Display API instance.

### `iPaperDisplayApiReady`

This event is emitted when the Display JavaScript API has successfully instantiated and populates the global scope with the `iPaperDisplayApi` object. At this point of time, all magic commands for the Display JavaScript API is accessible.

```js
document.addEventListener('iPaperDisplayApiReady', function () {
    // At this point in time, window.iPaperDisplayApi is available in the global scope
    window.iPaperDisplayApi.show();
});
```

### `iPaperDisplayInstanceReady`

This event is emitted when the Display JavaScript API has successfully loaded a Display instance and the instsance is now visible and ready to be interacted with. At this point, the user should be able to interact (scroll, click, etc.) with the Display instance shown on the side.

```js
document.addEventListener('iPaperDisplayInstanceReady', function () {
    // At this point in time, the Display Instance is ready to be interacted with
});
```

{% include note.html content="Due to the nature of the UI/UX of Display, the <code>iPaperDisplayInstanceReady</code> event is only fired if your user is originating from a desktop or tablet device. Mobile devices are redirected to the actual URL of the Display, where interaction with the API is not possible." %}
