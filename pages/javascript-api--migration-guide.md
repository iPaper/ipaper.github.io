---
permalink: /javascript-api/migration-guide
title: Migration Guide
summary: Migration guide from legacy v1 API to the new v2 API
---

## Step 1: Load the JavaScript API on the parent window

The legacy v1 API requires that the parent window and the iframed flipbook share the same origin: this is because strict CORS policy only allows iframed pages to access properties in the parent window if they belong to the same origin. v2 API circumvents this issue by using the modern `window.postMessage()` API.

Add the following script to either the `<head>` or `<body>` element in the parent window. The precise placement does not matter, because it asynchronously loads the API:

<!-- Note: this embed script is still provisional, depending on the decision in dev on where the script should be hosted and how it should be served -->
```html
<script type="text/javascript">
    (function(i,P,a,p,e,r){if(i.getElementById(a=a+'-'+e))return;
    r=i.querySelector(P).parentNode.appendChild(i.createElement(P));
    r.id=a;r.async=1;r.src=p+'?t='+(+new Date)})
    (document,'script','ipaper-embeds','https://viewer.ipaper.localhost/dist/api.bundle.js');
</script>
```

## Step 2: Update the setup of your API

The v2 API exposes a global object in the `window` called `iPaperAPI`. This is known as the default instance of the API, and targets the first available iframe on the page that loads an iPaper flipbook.

In the legacy v1 API, this is how it was done:

```html
<script type="text/javascript">
    document.domain = 'frontend.dk';

    function iPaperInit(api) {
        // ...
    }
</script>
```

In the new v2 API, we recommend doing this instead:

```html
<script type="text/javascript">
    function iPaperInit() {
        // ...
    }
</script>
```

Note that you no longer:
- need to specify `document.domain` due to relaxation of CORS requirement for `postMessage()`, and
- have access to the `api` argument made available in the `iPaperInit()` method&mdash;this is replaced by the `iPaperAPI` global variable

## Step 3: Ensure that your commands and events are modified

Commands and events are no longer namespaced by module. In the legacy v1 API, the `Publication` and `Shop` namespaces are available. The new v2 API collapses these namespaces since there is no risk of naming clashes&mdash;this also greatly simplifies how your page can interact with an iframed flipbook.

The following table maps the old commands to new ones available in v2 API:

| Namespace   | Old name   | New name   | Note                    |
|=============|============|============|=========================|
| Publication | `gotoPage` | `goToPage` | Camel-casing updated    |
| Shop        | `addItem`  | `addItem`  | *Event was not renamed* |

The following table maps the old events to new ones available in v2 API:

| Namespace   | Old name               | New name             | Note                    |
|=============|========================|======================|=========================|
| Publication | `onPageElementClicked` | `onPageElementClick` | Tense changed           |
| Publication | `onSpreadChanged`      | `onSpreadChange`     | Tense changed           |
| Shop        | `addItem`              | `onItemAdd`          | Nomenclature changed    |
| Shop        | `onBasketClick`        | `onBasketClick`      | *Event was not renamed* |

```js
document.domain = 'frontend.dk';

function iPaperInit(api) {
    // Event listener
    api.Shop.addEventListener("addItem", function(data) {
        console.log("Item added: " + data.title);
    });

    // Dispatch command when a button is clicked
    document.getElementById('button').addEventListener('click', function() {
        api.Publication.gotoPage(4);
    });
}
```

In the new v2 API, we recommend doing this instead:

```js
function iPaperInit() {
    // Event listener triggers magic callback
    iPaperAPI.onItemAdd = function(data) {
        console.log("Item added: " + data.title);
    };

     // Dispatch command when a button is clicked
    document.getElementById('button').addEventListener('click', function() {
        iPaperAPI.goToPage(4);
    });
}
```