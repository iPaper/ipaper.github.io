---
title: Iframing Flipbooks
permalink: /flipbook/integration/iframing-flipbooks
redirect_from:
  - /integration/iframing-flipbooks
  - /display/DOC/iframing+Catalogs
tags: Flipbook
---

<div class="alert alert-warning">
	<i class="fa fa-warning"></i>
	<b>Important:</b>

	While it is possible to do, we generally do not recommend iframing catalogs unless you have a specific reason for doing so.
	<ul>
		<li>As visitors come from a multitude of devices, including tablets, phones, and desktops, you’ll have to handle the different screen sizes yourself.</li>
		<li>Tablets and phones have special requirements to ensure they work when users rotate their device.</li>
		<li>The smaller the catalog is, the harder it is for users to read it. By opening up catalogs in a new window, rather than in an iframe, you ensure the users get the best possible reading experience.</li>
	</ul>

	This being said, if you want or need to embed the flipbook in an <code>&lt;iframe&gt;</code> element, please make sure to read and understand the following guide carefully.
</div>

## A brief note on domains

For best results, the flipbook you wish to embed should exist on a subdomain to the domain on which the iframe is placed.
A [working Branded Domain module](https://help.ipaper.io/en/articles/1857338-how-can-i-show-flipbooks-on-my-own-domain-branded-domain) is required for this.
If you embed the flipbook using the iPaper-branded URL, we cannot offer support for it and weird cross-device behavior can be expected.


## Foreword

When using iframes on mobile devices it can be tricky trying to make it respond as expected. Below we show you how to make flipbooks behave optimally.

{% include important.html content="
	It’s important that you follow our directions below precisely. There are many devices and what may work for you in testing will fail for users in production. If you manage to get something working that isn’t described here, do tell us so we can verify the solution. Anything but the below is to be considered unsupported and may fail either nor or in the future.
"%}

## Allow autoplaying and fullscreen access in video enrichments

In order to allow elements in the flipbook to do the following when it is iframed:

1. Autoplay videos without hindrance, and
2. Have access to the fullscreen API (e.g. embedded videos from Vimeo/YouTube or native MP4 videos) 

&hellip;the `<iframe>` element needs to allow these explicitly by means of specifying a [feature policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Feature_Policy). This is done by adding the following attributes to the element:

* `allow="autoplay; fullscreen;"`
* `allowfullscreen` (for backwards compatbility)
* `webkitallowfullscreen` (for backwards compatbility)
* `mozallowfullscreen` (for backwards compatbility)

Therefore, your `<iframe>` source will look a little like this, with `YOUR_FLIPBOOK_URL` replaced with the absolute URL of the flipbook you want to embed on your page:

```
<iframe
  src="YOUR_FLIPBOOK_URL"
  allow="autoplay; fullscreen;"
  allowfullscreen
  webkitallowfullscreen
  mozallowfullscreen></iframe>
```

## Embedding flipbooks in specific sizes

### 100%&times;100% size (full viewport size)

{% include note.html content="This is supported on all platforms and is the recommended way of iframing catalogs."%}

In order to iframe a iPaper catalog, spanning 100% of page, we need to use a specific setup. The markup below shows the essence of what is needed. Firstly, if we set the `<iframe>` element to have the width and height of 100% we must place this inside a div. Having done this we need to do the following:

* Doctype must be `<!DOCTYPE html>`
* Set the wrapper `<div>` width and height to 100%.
* Set the wrapper `<div>` overflow to hidden.
* Set `<body>` and `<html>` height to 100%.
* Include the `<meta>` tag presented below.
* Include the `<script>` tag presented below, setting the document.domain to the root domain used.

{% include important.html content="The steps listed above must be ready on load. It will NOT work if you manipulate the DOM client-side."%}

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" style="height: 100%">
  <head>
    <title>Catalogues</title>
    <style type="text/css">
        * { margin: 0; padding: 0; }
    </style>
    <script type="text/javascript">document.domain = 'ipapercms.dk';</script>
    <meta name="viewport" content="initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no, width=device-width" />
  </head>
    <body style="height: 100%">
        <div style="height: 100%; width: 100%; overflow: hidden">
            <iframe
                src="http://test.ipapercms.dk/Releases/Mobile/"
                scrolling="no"
                frameborder="0"
                style="width: 100%; height: 100%"
                allow="autoplay; fullscreen;"
                allowfullscreen
                webkitallowfullscreen
                mozallowfullscreen></iframe>
        </div>
    </body>
</html>
```

### Non-100%&times;100% size

{% include important.html content="This is only supported for the <b>iPad</b> and <b>Desktop</b> platforms. On all other platforms it is unsupported. While you may get it to work, expect it to break on certain devices and later on when we change the system."%}

For these platforms you can specify width in any size you want, even in percentages. Do take care to leave enough space for the user to have a usable experience however. To set the size, you need to change the dimensions on the outer div like this:

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" style="height: 100%">
  <head>
    <title>Catalogues</title>
    <style type="text/css">
        * { margin: 0; padding: 0; }
    </style>
    <script type="text/javascript">document.domain = 'ipapercms.dk';</script>
    <meta name="viewport" content="initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no, width=device-width" />
  </head>
    <body style="height: 100%">
        <div style="height: 300px; width: 600px; overflow: hidden">
            <iframe
                src="http://test.ipapercms.dk/Releases/Mobile/"
                scrolling="no"
                frameborder="0"
                style="width: 100%; height: 100%"
                allow="autoplay; fullscreen;"
                allowfullscreen
                webkitallowfullscreen
                mozallowfullscreen></iframe>
        </div>
    </body>
</html>
```

### Dynamically Resizing
Dynamically resizing the div will work. Do make sure you resize the outer element and not the iframe.

### Removing the iPaper User Interface
To remove the iPaper user interface, go to <b>Settings > Design > Layout > Hide Standard UI</b>.   
Or have a look at [Query String Parameters](/integration/query-string-parameters#hidestandardui)   

{% include note.html content="All JavaScript events will still be fired, even without the user interface present."%}

## Troubleshooting

### There is unexpected whitespace around my flipbook
**Symptoms:** There is unexpected whitespace around the flipbook (either vertically or horizontally). When the viewport is resized to a smaller size, the padding proportionally decreases.

**Common causes:** The containing element of the `<iframe>` element or the `<iframe>` element itself has an explicit width that is too large compared to the maximum size we render the flipbook as.

**Solution:** Set a `max-width` or `max-height` property on the containing element of the `<iframe>` element to a specific value (for instance `720px`). Experiment with different values that work well on exactly your website and different window sizes.
