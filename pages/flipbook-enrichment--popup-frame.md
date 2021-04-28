---
title: Popup frame
permalink: /flipbook-enrichment/popup-frame
redirect_from: 
    - /integration/popup-frame
tags: Flipbook integration
---

## Security

The best precautions security-wise is to include both X-Frame-Options and Content-Security-Policy for full browser support. Read more about how this is done below.

### Security headers

To ensure that your content is safeguarded against [clickjacking](https://owasp.org/www-community/attacks/Clickjacking) we recommend using the HTTP headers, X-Frame-Options and Content-Security-Policy. In the case you have added preventive measures we check the embedded website before trying to serve the popup-frame in the Flipbook viewer. This ensures that we don't end up showing the enduser an error in the browser, if this site doesn't allow to be iframed we give the user an option to open the site in a new tab in the browser.

### X-Frame-Options

Due to the nature of `ALLOW-FROM` being deprecated in the major browsers this is no longer a viable solution for preventing clickjacking in flipbooks. To solve that issue you will have to refer to Content-Security-Policy.

### Content-Security-Policy

Applying Content-Security-Policy is a more complex task, as it can have implications on the content on your own site if not done correctly. If your only intent is to prevent clickjacking, the frame-ancestors directive can be applied without it having implications on your content. In the case of you not having a branded domain you should add `frame-ancestors viewer.ipaper.io` and in the case of you using a branded domain then you should of course use your branded domain instead.

As of the specification for Content-Security-Policy version 2 and 3 the value of frame-ancestors override any value set in X-Frame-Options if those specifications have been implemented by the browser.
For further information about Content-Security-Policy click here [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

## Closing a popup from the frame page

It is possible for a frame page to close its popup. To do this, you simply have to execute the following JavaScript in the page that is framed.

```javascript
parent.postMessage('closePopup', '*');
```

If you want, you can pass additional parameters to the close command to update the basket count of the basket icon in the flipbook, as well as displaying the product name of the product that was added.

```javascript
parent.postMessage({ 
    command: 'closePopup',
    productName: 'White lamp', /*optional*/
    basketCount: 3 /* optional */
}, '*');
```

## Workarounds for iOS browser caveats

These workarounds apply to all browsers on iOS (namely Safari and any other third-party browsers), because they all use the same WebKit rendering engine on iOS.

### Iframed page jumping to top

Certain pages may occasionally jump to the top when iframed within a popup frame. It is often triggered by repaint events in the browser that involve changing the height of the page, as well as on pages that are excessively large. It is probably due to the iOS browser not being able to calculate the actual height of the `<iframe>` element properly.

To circumvent this issue, we recommend adding the following styles to the stylesheet of the page that is embedded in the popup frame:

```css
html, body {
    height: 100%;
    overflow: auto;
    -webkit-overflow-scrolling: touch;
}
```

### Page in popup frame appears too wide

Depends on how a page&rsquo;s width is set in the stylesheet, there is a possibility that certain pages, when embedded within an `<iframe>` and viewed on iOS browsers, will appear too large and hence overflow from its original bounds.

In iOS browsers, `<iframe>` elements cannot be restricted by size: declaring explicit width and height in CSS does not work. The browser will instead attempt to size the `<iframe>` so that all its content becomes visible. This has proven to be problematic for a small subset of pages, especially those containing wide content that are dynamically resized by JavaScript.

We recommend adding `max-width: 100vw` to the body element of the embedded page, which will force the `<iframe>` to be aware of the size of its wrapping container. It effectively places a constraint on the maximum permissible width for the page:

```css
body {
    max-width: 100vw;
}
```

## See also

[OWASP Guide to Clickjacking defense](https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking_Defense_Cheat_Sheet.html)
