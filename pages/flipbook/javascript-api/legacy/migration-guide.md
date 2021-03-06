---
title: Migration Guide
permalink: /flipbook/javascript-api/legacy/migration-guide
redirect_from: /flipbook-javascript-api/migration-guide
summary: Migration guide from legacy v1 API to the new v2 Flipbook API
tags: Flipbook JS API
---

## Step 1: Load the Flipbook JavaScript API on the parent window

The legacy v1 API requires that the parent window and the iframed flipbook share the same origin: this is because strict CORS policy only allows iframed pages to access properties in the parent window if they belong to the same origin. v2 Flipbook API circumvents this issue by using the modern `window.postMessage()` API.

Add the following script to either the `<head>` or `<body>` element in the parent window. The precise placement does not matter, because it asynchronously loads the API. [Please refer to this help article](https://intercom.help/ipaper/do-more-with-ipaper/the-ipaper-api-javascript) on how to obtain the iPaper Flipbook API script from the admin. The generated code will look something as follow:

```html
<!-- Start of async iPaper Flipbook API script -->
<script>
(function(i,P,a,p,e,r){if(i.getElementById(a=a+'-'+e))return;
r=i.querySelector(P).parentNode.appendChild(i.createElement(P));
r.id=a;r.async=1;r.src=p+'/'+e+'.js'})
(document,'script','ipaper-api','<ApiBaseUrl>','<ApiSecret>');
</script>
<!-- End of async iPaper Flipbook API script -->
```

{% include note.html content="Both `<ApiBaseUrl>` and `<ApiSecret>` in the snippet above will be substituted with partner and license-dependent configurations and be automatically populated, when you retrieve the API script from the admin." %}

## Step 2: Update the setup of your Flipbook API

The v2 Flipbook API exposes a global object in the `window` called `iPaperAPI`. This is known as the default instance of the API, and targets the first available iframe on the page that loads an iPaper flipbook.

In the legacy v1 API, this is how it was done:

```html
<script type="text/javascript">
    document.domain = 'frontend.dk';

    function iPaperInit(api) {
        // ...
    }
</script>
```

In the new v2 Flipbook API, we recommend doing this instead:

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

Commands and events are no longer namespaced by module. In the legacy v1 API, the `Publication` and `Shop` namespaces are available. The new v2 Flipbook API collapses these namespaces since there is no risk of naming clashes&mdash;this also greatly simplifies how your page can interact with an iframed flipbook.

The following table maps the old commands to new ones available in v2 Flipbook API:

| Namespace   | Old name                    | New name                          | Note                    |
| ----------- | --------------------------- | --------------------------------- | ----------------------- |
| Publication | [`gotoPage`](./v1#gotopage) | [`goToPage`](./commands#gotopage) | Camel-casing updated    |
| Shop        | [`addItem`](./v1#additem)   | [`addItem`](./commands#additem)   | *Event was not renamed* |

The following table maps the old events to new ones available in v2 Flipbook API:

| Namespace   | Old name                                            | New name                                            | Note                    |
| ----------- | --------------------------------------------------- | --------------------------------------------------- | ----------------------- |
| Publication | [`onPageElementClicked`](./v1#onpageelementclicked) | [`onPageElementClick`](./events#onpageelementclick) | Tense changed           |
| Publication | [`onSpreadChanged`](./v1#onspreadchanged)           | [`onSpreadChange`](./events#onspreadchange)         | Tense changed           |
| Shop        | [`addItem`](./v1#additem-1)                         | [`onItemAdd`](./events#onitemadd)                   | Nomenclature changed    |
| Shop        | [`onBasketClick`](./v1#onbasketclick)               | [`onBasketClick`](./events#onbasketclick)           | *Event was not renamed* |

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

In the new v2 Flipbook API, we recommend doing this instead:

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

## Step 4: Ensure that you are using updated camel-cased keys when parsing payloads

If you have code that depends on payload(s) returned from the legacy v1 API, note that we have now standardized casing for all keys in payload objects:

### Adding an item programmatically to the shop basket (command)

Used by [`addItem` (v1)](./v1/#additem) and [`addItem` (v2)](./events#onitemadd).

| Old property name | New property name | Note                           |
| ----------------- | ----------------- |------------------------------- |
| `productID`       | `productId`       | "ID" has been changed to "Id"  |

### When an item has been added to the shop basket (event)

Used by [`addItem` (v1)](./v1/#additem) and [`onItemAdd` (v2)](./events#onitemadd).

| Old property name | New property name | Note                           |
| ----------------- | ----------------- |------------------------------- |
| `productID`       | `productId`       | "ID" has been changed to "Id"  |

### When a page element is clicked in the iframed flipbook (event)

Used by [`onPageElementClicked` (v1)](./v1/#onpageelementclicked) and [`onPageElementClick` (v2)](./events#onpageelementclick).

| Old property name      | New property name      | Note                                                                |
| ---------------------- | ---------------------- |-------------------------------------------------------------------- |
| `data.productID`       | `data.productId`       | "ID" has been changed to "Id"                                       |
| `data.amountselection` | `data.amountSelection` | "amountselection" has been changed to camel-cased "amountSelection" |
| `data.packagesize`     | `data.packageSize`     | "packagesize" has been changed to camel-cased "packageSize"         |

## Step 5: Update event settings instead of returning from dispatchers

If you have used the legacy v1 API to modify event behaviours in the iframed flipbook, note that the protocol has now changed. In the legacy v1 API, these settings are actually concatenated if multiple event handlers are defined, resulting in potentially confusing behavior. To circumvent this issue, we have added a new command in v2 Flipbook API that allows you to explicitly define default behaviors of flipbook events: [`updateEventSettings`](./commands#updateeveentsettings).

In the legacy v1 API, if you want to stop the basket from opening when the icon is clicked, this is what was recommended:

```js
function iPaperInit(api) {
    api.Shop.addEventListener("addItem", function(data) {
        console.log("Item added: " + data.title);

        return {
            preventDefault: true
        }
    });
}
```

In v2 Flipbook API, this is a **global** setting on the flipbook but can be modified at any time. It is to be set outside the event handler, because if done within the event handler, the event's default action would have already been invoked and can no longer be intercepted.

```js
function iPaperInit() {
    // Magic command to modify event settings in iframed flipbook
    iPaperAPI.updateEventSettings({
        onItemAdd: { preventDefault: true }
    });

    // Listen to `onItemAdd` event
    iPaperAPI.onItemAdd = function(data) {
        console.log("Item added: " + data.title);
    };
}
```

The advantage of this new approach is that you can then dynamically update the settings whenever you want. Let's say that if you want to re-enable the add item default action when a button is clicked, you can simply do this:

```js
function iPaperInit() {
    // Magic command to modify event settings in iframed flipbook
    iPaperAPI.updateEventSettings({
        onItemAdd: { preventDefault: true }
    });

    // Listen to `onItemAdd` event
    iPaperAPI.onItemAdd = function(data) {
        console.log("Item added: " + data.title);
    };

    // Re-enable default event when a button is clicked
    document.querySelector('button#enable-shop-action').addEventListener('click', function() {
        iPaperAPI.updateEventSettings({
            onItemAdd: { preventDefault: false }
        });
    });
}
```