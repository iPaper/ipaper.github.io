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
2. An arbitrary Display instance

#### 1. Showing a Display instance associated with a URL

If the current page matches the CTA button URL pattern, you can simply use the `show()` magic command without any arguments to show a Display instance associated with the URL:

```js
/*
 * Show the Display instance that is associated with a particular URL
 * NOTE: This only works if the current page already has a Display instance associated with it.
 */
window.iPaperDisplayApi.show();
```

#### 2. Showing an arbitrary Display instance

For the second scenario is useful when you have the Display JS API embedded on your page, but has no Display instance associated with it because it does not match the CTA button URL pattern. By invoking `show(<guid>)`, where `guid` refers to the GUID of your Display instance of choice, you can show any arbitrary Display instance associated with your license on that page. Your GUID will be in the format of `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`.

```js
/*
 * Show an arbitrary Display instance
 * NOTE: The GUID of your Display instance can be inferred from its canonical URL in the following format:
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
2. An arbitrary Display call-to-action button

#### 1. Showing a Display call-to-action button associated with a URL

```js
/*
 * Show the Display call-to-action button that is associated with a particular URL
 * NOTE: This only works if the current page already has a Display instance associated with it.
 */ 
window.iPaperDisplayApi.showButton();
```

#### 2. Showing an arbitrary Display call-to-action button

```js
/*
 * Show an arbitrary Display call-to-action button
 * NOTE: The GUID of your Display instance can be inferred from its canonical URL in the following format:
 * - https://display.ipaper.io/<license>/<guid>
 */
window.iPaperDisplayApi.showButton(<guid>);
```

### `hideButton`

The `hide()` magic command does not accept any arguments, and simply hides the Display call-to-action button away:

```js
window.iPaperDisplayApi.hideButton();
```