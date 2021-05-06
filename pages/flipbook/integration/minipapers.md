---
title: Minipapers
permalink: /flipbook/integration/minipapers
redirect_from:
    - /integration/minipapers
    - /display/DOC/Minipapers
tags: Flipbook integration
---

## Description

Minipapers is a method for which to easily embed a miniaturized version of a flipbook on your website. The following view options are available:

* **Perspective**&mdash;displays a three-dimensional flipbook
* **Single page**&mdash;displays a single page on the flipbook
* **Spread**&mdash;displays a spread on the flipbook
* **Page slider**&mdash;displays an animated slider showing pages and spreads of a pre-defined page range

Once integrated on your website, clicking on a minipaper will redirect the user to the actual flipbook being displayed.

## Redirecting to an alternative URL

It is possible to override the default link action and target when a user clicks on the embedded minipaper. This behavior can be configured by appending relevant query strings to the URL found in the `src` attribute of the `<iframe>` element in the embed code. For example, given the following embed snippet:

```html
<!-- iPaper snippet start -->
<iframe
    style="display: block;"
    src="<MinipaperEmbedUrl>"
    scrolling="no"
    frameborder="0"></iframe>
<!-- iPaper snippet end -->
```

The URL to be modified will be the string `<MinipaperEmbedUrl>`. The following query strings are supported:

| Key              | Accepted values                      | Default value                  | Description |
|==================|======================================|================================| ============|
| `targetUrl`      | `string`                             | The public URL of the flipbook | Changes the URL that users are redirected to when an embedded minipaper is clicked on. The URL must be fully qualified, starting with `http://` or `https://`, and be [URL encoded](https://en.wikipedia.org/wiki/Percent-encoding).<br /><br />Example:<br />`<MinipaperEmbedUrl>?targetUrl=https%3A%2F%2Fipaper.io%2F` |
| `target`         | `_self`, `_blank`, `_parent`, `_top` | `_blank`                       | Changes the behavior of the anchor element that determines where to display the linked URL. [Read more about the specification for `target` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#target).<br /><br />Example:<br />`<MinipaperEmbedUrl>?target=_self` |

If you want multiple query string keys to be attached to the URL, you can separate them using the `&` character, i.e.: `<MinipaperEmbedUrl>?targetUrl=<Url>&target=<Target>`. The order of the queries does not matter.

{% include note.html content="As per specification, **all values in query strings must be properly [URL-encoded](https://en.wikipedia.org/wiki/Percent-encoding)**. There are several online tools for encoding text for use in query strings, for example: [https://meyerweb.com/eric/tools/dencoder/](https://meyerweb.com/eric/tools/dencoder/)." %}

## Preserving aspect ratio

If you want to preserve the aspect ratio of the embedded minipaper, so that it is scaled proportionately in a page with responsive design, we suggest using the [`padding-bottom` trick](https://css-tricks.com/aspect-ratio-boxes/), which will force an aspect ratio of your choice on the surrounding container. The element displaying the minipaper&mdash;the `<iframe>` element&mdash;should then be positioned absolutely relative to this container.

For example, if a 2:1 ratio is desired for a container, `padding-bottom: 50%` should be used:

```html
<div style="position: relative; width: 100%; padding-bottom: 50%;">
    <!-- iPaper snippet start -->
    <iframe
        style="display: block; width: 100%; height: 100%;"
        src="<MinipaperEmbedUrl>"
        scrolling="no"
        frameborder="0"></iframe>
    <!-- iPaper snippet end -->
</div>
```