---
permalink: /javascript-api/advanced-usage
title: Advanced Usage
---

## Multiple Flipbooks

In use cases where multiple flipbooks are to be embedded on the same page, small changes to the markup is required so that each individual instances will reference the correct `<iframe>` element without conflict.

The minimal config design of our API means that it will attempt to look for an `<iframe>` containing a flipbook automatically without any additional configuration from the user and create a new instance from said element. When multiple flipbooks are present on the same page, this strategy may not work due to race conditions. Therefore, two actions will be required:

1. **Identify the default flipbook.** The default flipbook (which will be accessible by the `iPaperAPI` variable) using the HTML5 data- attribute, `data-ipaper`:

    ```html
    <iframe src="https://demo.ipaper.io" data-ipaper></iframe>
    ```

    This iframed flipbook will then be accessible via the globally defined API instance `iPaperAPI`, just like in the single flipbook use case outlined in [quick-start](./quick-start).

    {% include warning.html content="If `data-ipaper` attribute is not added, then the default API instance will simply select the **first** `<iframe>` containing a flipbook that reports back, presenting a race condition. **We cannot guarantee that this is always the first visible flipbook on the page.**" %}


2. **Instantiate APIs for subsequent flipbooks.** Subsequent flipbooks will need to added to manually instantiated API constructor manually. The API constructor is exposed via the `_iPaperAPI` (note the preceeding underscore character), and a new instance can be created on an `<iframe>` element by passing the element as the first argument:

    ```js
    var anotherIPaper = document.getElementById('another-flipbook')
    var anotherIPaperAPI = new _iPaperAPI(anotherIPaper);
    ```

### Example

```html
<!doctype html>
<html>
<head>
    <title>Multiple iframed iPapers</title>

    <!-- Start of async iPaper API code -->
    <!-- NOTE: The entire code snippet below can be obtained directly from the Admin. Refer to our help article for further information -->
    <script>
    (function(i,P,a,p,e,r){if(i.getElementById(a=a+'-'+e))return;
    r=i.querySelector(P).parentNode.appendChild(i.createElement(P));
    r.id=a;r.async=1;r.src=p+'/'+e+'.js'})
    (document,'script','ipaper-api','<ApiBaseUrl>','<YourApiKey>');
    </script>
    <!-- End of async iPaper API code -->

    <script>
        functon iPaperInit() {
            // Listen to event from the default iframe flipbook
            // This is the default API instance
            iPaperAPI.onSpreadChange = function(data) {
                console.log('onSpreadChange event detected in default flipbook', data);
            };

            // Listen to event from a second iframe flipbook
            // Create new API instance first
            var anotherIPaper = document.getElementById('yet-another-flipbook')
            var anotherIPaperAPI = new _iPaperAPI(anotherIPaper);
            anotherIPaperAPI.onSpreadChange = function(data) {
                console.log('onSpreadChange event detected in second flipbook', data);
            };
        }
    </script>
</head>
<body>
    <!-- Remember to add the HMTL5 `data-ipaper` attribute to the default iframe -->
    <iframe src="https://demo.ipaper.io" style="width: 100%; height: 400px;" data-ipaper></iframe>

    <!-- Subsequent iframes can be identified by any means, but we use ID for convenience -->
    <iframe src="https://demo.ipaper.io" style="width: 100%; height: 400px;" id="yet-another-flipbook"></iframe>
</body>
</html>
```

## Event listeners and command triggers

If you are more accustomed to working with event listeners and command triggers, and do not want to use magic callbacks and commands that are available via the API instance, you can simply:

- add event listeners to the `<iframe>` element, and/or
- trigger commands using `.trigger(<commandName>, <argument>)`

The event name that the event listeners should check with are specified in [events](./events), while command names are specified in [commands](./commands). Mismatched event/command names will simply do nothing.

```html
<!doctype html>
<html>
<head>
    <title>Example iPaper JS API use</title>

    <!-- Start of async iPaper API code -->
    <!-- NOTE: The entire code snippet below can be obtained directly from the Admin. Refer to our help article for further information -->
    <script>
    (function(i,P,a,p,e,r){if(i.getElementById(a=a+'-'+e))return;
    r=i.querySelector(P).parentNode.appendChild(i.createElement(P));
    r.id=a;r.async=1;r.src=p+'/'+e+'.js'})
    (document,'script','ipaper-api','<ApiBaseUrl>','<YourApiKey>');
    </script>
    <!-- End of async iPaper API code -->
    
    <script>
        functon iPaperInit() {
            // Listen to the `onSpreadChange` event emitted from the <iframe> element
            // Note: This is equivalent to `iPaperAPI.onSpreadChange = function(data) { ... }`;
            document.getElementById('my-ipaper-flipbook').addEventListener('onSpreadChange', function(data) {
                console.log(data);
            });

            // Navigate to page 4 when a button is clicked
            document.getElementById('page-4-button').addEventListener('click', function() {
                // Note: This is equivalent to `iPaperAPI.goToPage(4)`
                iPaperAPI.trigger('goToPage', 4);
            });
        }
    </script>
</head>
<body>
    <iframe
        src="https://demo.ipaper.io"
        style="width: 100%; height: 400px;"
        id="my-ipaper-flipbook"></iframe>
    <button type="button" id="page-4-button">Go to page 4</button>
</body>
</html>
```