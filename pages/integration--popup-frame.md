---
title: Popup content
permalink: /integration/popup-content
redirect_from: "/display/DOC/Popup+content"
---

## Sizing
The content of the iframe reflows, so no scale is applied.

## Images
Large images automatically shrink to iframe width.

## Talking to the iPaper API
You cannot communicate with the iPaper API.

## Rotation/resizing
The popup content wrapper has the following constraints:

```
max-width:	600px;
min-width: 	200px;
min-height:	250px;
```

Content wrapper will resize itself, to fit inside the browser window, until it reaches a max/min width. Height is set based on content height, and window height. When content is taller than window, content will scroll. When the window is taller than the content, the content wrapper will set height based on content height.

## CSS applied 
```css
html, body, h1, h2, h3, p {
    margin: 0;
    padding: 0;
    font-family: Verdana, Arial, Sans-Serif;
}
body {
    padding: 10px;
    -webkit-transform-style: preserve-3d;
    -webkit-text-size-adjust: 100%;
}
p {
    line-height: 20px;
    margin-bottom: 10px;
    font-size: 14px;
}
hr {
    border: none;
    border-top: 1px solid #CCC;
    margin-top: 12px;
    display: block;
    height: 10px;
}
img {
    max-width: 100%;
    height: auto !important;
}
```