---
permalink: /javascript-api/quick-start
title: Quick Start
summary: The v2 JavaScript API allows for streamlined interaction with iframed flipbooks using cross-origin communications available in modern browsers.
---

## Overview

The v2 JavaScript API uses the [`window.postMessage` API](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage) for two-way communications between the parent window and one or more flipbooks embedded in the parent window inside `<iframe>` elements. For this to work, you will need to include the API script on your page:

<!-- Note: this embed script is still provisional, depending on the decision in dev on where the script should be hosted and how it should be served -->
```html
<script type="text/javascript">
    (function(i,P,a,p,e,r){if(i.getElementById(a=a+'-'+e))return;
    r=i.querySelector(P).parentNode.appendChild(i.createElement(P));
    r.id=a;r.async=1;r.src=p+'?t='+(+new Date)})
    (document,'script','ipaper-embeds','https://viewer.ipaper.localhost/dist/api.bundle.js');
</script>
```

## Zero-config setup

Most of our customers use our API to interact with a single instance of a flipbook on their page. A frictionless zero-config setup is therefore implemented, meaning that for use-cases of single flipbooks iframed on a single page, no additional configuation is required and you can start interacting with the iframed flipbook immediately. The setup will automatically identify the first iframed flipbook on the page, which can have a minimal markup as such:

```html
<iframe src="https://demo.ipaper.io"></iframe>
```

## Interacting with iframed flipbook

The embedded script will call the `iPaperInit()` method that is defined globally in the parent window, and you can then interact with the iframed flipbook via the `iPaperAPI` instance created by default:

```html
<!doctype html>
<html>
<head>
    <title>Example iPaper JS API use</title>
    <script type="text/javascript">
        (function(i,P,a,p,e,r){if(i.getElementById(a=a+'-'+e))return;
        r=i.querySelector(P).parentNode.appendChild(i.createElement(P));
        r.id=a;r.async=1;r.src=p+'?t='+(+new Date)})
        (document,'script','ipaper-embeds','https://viewer.ipaper.localhost/dist/api.bundle.js');
    </script>
    <script>
        functon iPaperInit() {
            // Define a callback for the `onSpreadChange` event
            // `iPaperAPI` is the default first instance of the API
            iPaperAPI.onSpreadChange = function(data) {
                console.log(data);
            }

            // Navigate to page 4 when a button is clicked
            document.getElementById('page-4-button').addEventListener('click', function() {
                iPaperAPI.goToPage(4);
            });
        }
    </script>
</head>
<body>
    <iframe src="https://demo.ipaper.io" style="width: 100%; height: 400px;"></iframe>
    <button type="button" id="page-4-button">Go to page 4</button>
</body>
</html>
```

The `iPaperAPI` object exposes several methods that can be grouped into two categories: [**magic event callbacks**](./events) and [**magic commands**](./commands).

- **Events happen on the flipbook and are emitted to the parent window**, which triggers magic callbacks. An example of a flipbook event is the [`onSpreadChange`](./events#onspreadchange) event. [Read more](./events) about how to listen to these events and react to them accordingly.
- **Commands are instructions issued from the parent window to the flipbook**, done via invoking magic commands. An example of a flipbook command is the [`goToPage`](./commands#gotopage) method. [Read more](./commands) about how to issue commands to instruct your iframed flipbook to perform specified actions.

## Multiple flipbooks

In the event that multiple flipbooks are to be embedded via `<iframe>` on the same page, some workarounds are required. Refer to the [**Multiple Flipbooks**](./advanced-usage#multiple-flipbooks) section for further implementation details.