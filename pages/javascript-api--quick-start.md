---
permalink: /javascript-api/quick-start
title: Quick Start
summary: The v2 JavaScript API allows for streamlined interaction with iframed flipbooks using cross-domain communications available in modern browsers.
---

## Overview

The v2 JavaScript API uses the postMessage API for two-way communications between the parent window and one or more flipbooks embedded in the parent window inside `<iframe>` elements. For this to work, you will need to include the API script on your page:

```html
<script type="text/javascript">

</script>
```

## Zero-config setup

Most of our customers use our API to interact with a single instance of a flipbook on their page. A frictionless zero-config setup is therefore implemented, meaning that for use-cases of single flipbooks iframed on a single page, no additional configuation is required and you can start interacting with the iframed flipbook immediately.

The embedded script will call the `iPaperInit()` method that is defined globally in the parent window, and you can then interact with the iframed flipbook via the `iPaperAPI` instance:

```html
<!doctype html>
<html>
<head>
    <title>Example iPaper JS API use</title>
    <script>
        functon iPaperInit() {
            // Define a callback for the `onSpreadChange` event
            iPaperAPI.onSpreadChange = function(data) {
                console.log(data);
            }

            // Navigate to page 4 when a button is clicked
            document
                .getElementById('page-4-button')
                .addEventListener('click', function() {
                    iPaperAPI.goToPage(4);
                })
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