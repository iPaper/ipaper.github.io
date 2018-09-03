---
title: Query String Parameters
permalink: /integration/query-string-parameters
redirect_from: "/display/DOC/Query+String+Parameters"
---

Certain functions in Flipbooks can be invoked by including query string parameters in the Flipbook address. The following parameters are documented and supported. Any parameter not documented here is not supported and shold not be used and depended upon.

## ForceLanguage

Say you have an international catalog with visitors from many nationalities. In iPaper CMS you can only define one language for the user interface (though this can be used to auto-detect the users language), but using the ForceLanguage parameter, you can override the normal user interface language. Example URL that forces the language to French:
```
http://catalogs.company.com/Brochure/?ForceLanguage=fr
```
{% include note.html content="Please refer to iPaper Support if you need a specific language code. If you link to a non-existing language code, the catalog default will be used instead." %}


## GotoFirstSearchResult

If you don't want to link to a specific page number, but rather to the first page that contains a certain search term, the GotoFirstSearchResult parameter can be used. The following sample link would take the user to the first page containing the term "Century":
```
http://catalogs.company.com/Brochure/?GotoFirstSearchResult=Century
```
{% include note.html content="If the search term is not found, the user will be sent to the first page." %}

## HideNavigationBars

Using this setting you can override the "Hide Navigation Bars" setting on Flipbooks:
```
http://catalogs.company.com/Brochure/?HideNavigationBars=true
```
{% include note.html content="This does not work on mobile catalogs." %}


## HideStandardUI

Using this setting you can override the "Hide Standard UI" setting on Flipbooks:
```
http://catalogs.company.com/Brochure/?HideStandardUI=true
```
{% include note.html content="This does not work with Flash & mobile catalogs." %}

## Page

The Page parameter is used when you want to deeplink to a certain page in the catalog. The following sample link would take the user directly to page 15:
```
http://catalogs.company.com/Brochure/?Page=15
```
{% include note.html content="Linking to a non-existing page number will take the user to the first page instead." %}


## DisableScrollZoom
Using this setting you can disable zooming when users use their mouse wheel for scrolling:
```
http://catalogs.company.com/Brochure/?DisableScrollZoom=true
```
{% include note.html content="This will not affect Flash & mobile catalogs." %}

## Affiliate_

The Affiliate_ parameter that can be used for tracking ex. referrals. All query parameters starting with Affiliate_ will be appended to any external URL the iPaper contacts.
```
http://catalogs.company.com/Brochure/?Affiliate_X=Y
```

The value of X and Y are completely up to you, as they will not affect the actual Flipbook, but it will allow you to track which Flipbooks are requesting specific URLs on your site.
Consider the following example scenario:

* You email your customers with a link for a Flipbook. Every link becomes unique for each user, with the Affiliate_ parameter, such as http://catalogs.company.com/Brochure/?Affiliate_UserID=user@email.net
* The user opens the link to the Flipbook, and a some point clicks a link that points to http://company.com/Products/
* The Affiliate_ parameter is appended (with the "Affiliate_" part omitted), so that the actual URL opened is http://company.com/Products/?UserID=user@email.net
* On the given URL, you can now identify which user actually opened the link, by examining the "UserID" parameter.


## Polite load

Polite loading delays the loading of Flipbook pages until the page has finished loading. The setup requires that a small JavaScript is loaded into the header of your site.

```html
<script type="text/javascript" src="http://catalogs.company.com/politeload.js"></script>
```

Once the above script is included you must add the polite parameter to the URL you are requesting.

```html
<iframe src="http://catalogs.company.com/Brochure/?polite=true"></iframe>
```

## Preload pages

The preload parameter can be used to ensure that a Flipbook only loads the visible pages initially. Standard behavior would also preload the next/previous pages. When preload=minimal is enabled the preloading will start loading once the user pages for the first time.

```html
<iframe src="http://catalogs.company.com/Brochure/?preload=minimal"></iframe>
```
