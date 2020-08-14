---
permalink: /display-javascript-api/quick-start
title: Quick Start
summary: The v1 Display JavaScript API allows for streamlined interaction a Display instance
tags: Display JS API
---

## Overview

The v1 Display JavaScript API is used for client webpages to show and interact with iPaper Display instances. Display instances may be directly associated with a given URL by means of pattern matching of the current page URL against a pre-defined pattern in the call-to-action (CTA) button URL value provided.

### Display instance

A Display instance, also known as a &ldquo;Display&rdquo;, can be built from the iPaper Admin, if you have the Display module enabled. It is 400px wide and has an arbitrary height, depending on the amount of content in the instance.

### The call-to-action (CTA) button
For every Display instance, a call-to-action (CTA) button is associated with it. The instance and the CTA button can be toggled individually. In a typical zero-configuration ground state:

* if a Display instance is associated with a given URL, the CTA button will be shown on page load. Clicking on the button will reveal the Display instance, which will animate into the viewport from the left or right side offscreen. The Display API can be used to show/hide the button and the Display instance programmatically.
* if a given URL has no Display instance associated with it, no CTA button or Display instance will be shown. However, you can load a Display instance arbitrarily using this API.

The Display Javascript API [exposes magic commands](/display-javascript-api/commands) and [emits a custom event upon instantiation](/display-javascript-api/events).

## Setup

A Display instance and its CTA button can only be shown on pages that has the Display JavaScript API embedded. The Display API embed script will look something like this, with `<YourApiKey>` being substitued with partner and license-dependent configurations:

```html
<!-- Start of Async iPaper Display API script -->
<script>
(function(i,P,a,p,e,r){if(i.getElementById(a=a+'-'+e))return;
r=i.querySelector(P).parentNode.appendChild(i.createElement(P));
r.id=a;r.async=1;r.src=p+'/'+e+'.js'})
(document,'script','ipaper-display-api','//display.ipaper.io/api/v1','<YourApiKey>');
</script>
<!-- End of Async iPaper Display API script -->
```

{% include note.html content="`<YourApiKey>` in the snippet above will be substituted with partner and license-dependent configurations and be automatically populated, when you retrieve the API script from the admin." %}