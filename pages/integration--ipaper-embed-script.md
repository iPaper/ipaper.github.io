---
title: iPaper Embed Script
permalink: /integration/ipaper-embed-script
redirect_from: "/display/DOC/iPaper+Embed+Script"
tags: Flipbook integration
---

The iPaper embed script snippet is a small piece of JavaScript that you paste in to your webpages. It enables the iPaper service to inject Pop-ups into the pages where the embed script is present.

## Find your account specific embed script

1. Log in to your iPaper account.
2. Navigate to → 'Pop-ups'.
3. Click the 'Get embed script' button.
4. Click 'Copy script' to copy the embed script to the clipboard.

<img src="/images/embed-script-1.png" style="max-width:100%;max-height:100%"/>

*The embed script modal*

## Insert snippet on your website

The embed script should be inserted as the last element of the ```<body>``` tag on every webpage where you want Pop-ups to show. A typical use case would be to add the embed script to all pages on your website.
{% include note.html content="Browser loads webpages progressively, which means that the resources are loaded in order of their occurrence in the source code. It is a good practice to place nonessential scripts as the last elements of the webpage" %}

<img src="/images/embed-script-2.png" style="max-width:100%;max-height:100%"/>

If you are using some sort of CMS system, the chances are that you can use commonly shared footer element to add embed script on every page. This way you can have only one place, where the script is stored in your websites source code.

{% include note.html content="You don't need the embed script when adding Pop-ups to your Flipbooks" %}

## After you have added the embed script

Once the embed script is added to your website, you will start to see Pop-ups that match the URL you have defined.

## Final notes on embed script

### Same embed script for different Pop-ups under one license

Embed script are unique per license (login group). This means that all Pop-ups created under the same license will share the same embed script code. Therefore, there is no need to insert embed script with given API_KEY on one webpage (URL) more than once, even when there is more than one lead generation tool that should be displayed on that page.

{% include note.html content="You don't need the embed script when adding Pop-ups to your Flipbooks" %}

### Multiple embed scripts on same webpage

In some edge case scenarios there might be a reason to use different embed scripts (with unique API_KEY) on the same webpage. This might be the case when users from different login groups are maintaining lead generation tools for the same webpage. In such cases the rules of inserting the code into webpage stays the same: embed scripts should always be inserted as the last elements of the ```<body>``` tag.
