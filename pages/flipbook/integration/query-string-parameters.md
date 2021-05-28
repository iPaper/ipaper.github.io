---
title: Query String Parameters
permalink: /flipbook/integration/query-string-parameters
redirect_from:
    - /integration/query-string-parameters
    - /display/DOC/Query+String+Parameters
tags: Flipbook integration
---

Certain functions in Flipbooks can be invoked by including query string parameters in the Flipbook address. The following parameters are documented and supported. Any parameter not documented here is not supported and shold not be used and depended upon.

## ForceLanguage

Say you have an international catalog with visitors from many nationalities. In iPaper CMS you can only define one language for the user interface (though this can be used to auto-detect the users language), but using the ForceLanguage parameter, you can override the normal user interface language. Example URL that forces the language to French:
```
http://catalogs.company.com/Brochure/?ForceLanguage=fr
```
{% include note.html content="Please refer to iPaper Support if you need a specific language code. If you link to a non-existing language code, the catalog default will be used instead." %}


## GoToFirstSearchResult

If you do not want to link to a specific page number, but rather to the first page that contains a certain search term, the GoToFirstSearchResult parameter can be used. The following sample link would take the user to the first page containing the term "Century":
```
http://catalogs.company.com/Brochure/?GoToFirstSearchResult=Century
```
{% include note.html content="If the search term is not found, the user will be sent to the first page." %}

{% include warning.html content="If both `GoToFirstSearchResult` and [`GoToAndHighlightFirstSearchResult`](#gotoandhighlightfirstsearchresult) are specified in the URL, this query string value will be ignored." %}

## GoToAndHighlightFirstSearchResult

This query performs the same operation as [`GoToFirstSearchResult`](#gotofirstsearchresult) above, but has the additional ability to highlight the term on the page itself.

```
http://catalogs.company.com/Brochure/?GoToAndHighlightFirstSearchResult=Century
```

{% include note.html content="If both [`GoToFirstSearchResult`](#gotofirstsearchresult) and `GoToAndHighlightFirstSearchResult` are specified in the URL, this query string value will take precedence." %}

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

## Query string forwarding

To forward query strings to links, you can prefix query strings with `ipforward_`. We will strip the prefix and add your query strings to any outgoing links in the Flipbook. 

As an example, the below URL:

```html
http://catalogs.company.com/Brochure/?ipforward_YourParameter=x
```
Would result in external links decorated with your parameter: `YourParameter=x`

You can use the `ipforward_` prefix with any parameter you want. If someone follows a link within your Flipbook, the ipforward is stripped, so only your parameter is retained in the link. And you can of course add multiple parameters:  
`?ipforward_YourParameter=x&ipforward_YourOtherParameter=y`

