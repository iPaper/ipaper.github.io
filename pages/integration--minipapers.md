---
title: Minipapers
permalink: /integration/minipapers
redirect_from: "/display/DOC/Minipapers"
---

## Description

Minipapers is a method for which to easily embed a miniaturized version of a flipbook on your website. The following view options are available:

* **Perspective**&mdash;displays a three-dimensional flipbook
* **Single page**&mdash;displays a single page on the flipbook
* **Spread**&mdash;displays a spread on the flipbook
* **Page slider**&mdash;displays an animated slider showing pages and spreads of a pre-defined page range

Once integrated on your website, clicking a minipaper will redirect the user to the actual Fflipbook being displayed.

## Preserving aspect ratio

If you want to preserve the aspect ratio of the embedded minipaper, so that it is scaled proportionately in a page with responsive design, we suggest using the [`padding-bottom` trick](https://css-tricks.com/aspect-ratio-boxes/), which will force an aspect ratio of your choice on the surrounding container. The element displaying the minipaper&mdash;the `<iframe>` element&mdash;should then be positioned absolutely relative to this container.

For example, if a 2:1 ratio is desired for a container, `padding-bottom: 50%` should be used:

```html
<div style="position: relative; width: 100%; padding-bottom: 50%;">
    <!-- iPaper snippet start -->
    <iframe
        style="display: block; position: absolute; top:0; right: 0; bottom: 0; left: 0; width: 100%; height: 100%;"
        src="<MinipaperEmbedUrl>"
        scrolling="no"
        frameborder="0"></iframe>
    <!-- iPaper snippet end -->
</div>
```