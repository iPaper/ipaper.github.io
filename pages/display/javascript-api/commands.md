---
title: Commands
permalink: /display/javascript-api/commands
redirect_from: /display-javascript-api/commands
summary: Commands are instructions issued by the page to the Display JavaScript API. Commands can be invoked by calling magic methods, which can be accessed directly from the API instance.
tags: Display JS API
---

## Overview

Commands are issued by your page, using magic methods exposed by the Display API instance. As these magic commands are attached to the Display API instance, it is imperative that you ensure the Display API is successfully instantiated. You can either:

1. check if the API is present upon at invocation

    ```js
    // Example 1
    if (window.iPaperDisplayApi) {
        window.iPaperDisplayApi.show();
    }

    // Example 2
    window.iPaperDisplayApi && window.iPaperDisplayApi.show();
    ```

2. or listen to a custom event that signals that the API is ready to use.

    ```js
    document.addEventListener('iPaperDisplayApiReady', function () {
        // At the point in time, window.iPaperDisplayApi is available in the global scope
        window.iPaperDisplayApi.show();
    });
    ```

     See [Events page for further information](/display-javascript-api/events).

## Display instance

A Display instance will be shown in a full viewport height `<iframe>` element that will enter enter the viewport from the left or right of the screen, depending on the settings configured for the specific instance.

### `show`

This command can be used to show:

1. A Display instance that is already associated with a URL, by means of URL pattern matching against the CTA button URL pattern configured for a particular instance, or
2. An arbitrary Display instance for a URL with no Display instance associated with it

#### 1. Showing a Display instance associated with a URL
For the first scenario, the `show()` magic command does *not* accept any arguments&mdash;attempts to supply it with a custom guid will result in a warning in the console. It is not possible to replace a Display instance that is already associated with a particular URL, with another arbitrary instance belonging to your license.

```js
// Showing the Display instance that is associated with a particular URL
window.iPaperDisplayApi.show();
```

#### 2. Showing an arbitrary Display instance on a URL not associated with a Display instance

For the second scenario is useful when you have the Display JS API embedded on your page, but has no Display instance associated with it because it does not match the CTA button URL pattern. In this case, you are allowed to show any arbitrary Display instance associated with your license on that page, by means of invoking the magic command with a single argument which contains the guid of your Display instance of choice:

```js
/*
 * Showing an arbitrary Display instance for a URL not associated with any Display instances
 * The GUID of your Display instance can be inferred from its canonical URL in the following format:
 * - https://display.ipaper.io/<license>/<guid>
 */
window.iPaperDisplayApi.show(<guid>);
```

### `hide`

The `hide()` magic command does not accept any arguments, and simply hides the Display instance away:

```js
window.iPaperDisplayApi.hide();
```

## Display call-to-action button

### `showButton`

Similar to the `show()` magic command, this command can be used to show:

1. A Display call-to-action button that is already associated with a URL, by means of URL pattern matching against the CTA button URL pattern configured for a particular instance, or
2. An arbitrary Display call-to-action button for a URL with no Display instance associated with it

#### 1. Showing a Display call-to-action button associated with a URL

```js
// Showing the Display call-to-action button that is associated with a particular URL
window.iPaperDisplayApi.showButton();
```

#### 2. Showing an arbitrary Display call-to-action button on a URL not associated with a Display instance

```js
/*
 * Showing an arbitrary Display call-to-action button for a URL not associated with any Display instances
 * The GUID of your Display instance can be inferred from its canonical URL in the following format:
 * - https://display.ipaper.io/<license>/<guid>
 */
window.iPaperDisplayApi.showButton(<guid>);
```

### `hideButton`

The `hide()` magic command does not accept any arguments, and simply hides the Display call-to-action button away:

```js
window.iPaperDisplayApi.hideButton();
```