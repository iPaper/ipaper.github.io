---
title: Minipapers
permalink: /integration/minipapers
redirect_from: "/display/DOC/Minipapers"
---

## Description

Minipapers is a method for which to easily integrate and display a miniaturized version of an iPaper on your website, by pasting an HTML iframe tag.

```html
<iframe style="width:220px; height:160px" src="http://wwww.example.com/MyPaper/MiniPaperFrame.aspx?PA=2" allowtransparency="true" scrolling="no" frameborder="0"></iframe>
```

## Types

For Flipbook, there are 3 diffrent kinds of minipapers:
* **Static cover** - Displays a static image of a given page from the iPaper
* **Page flipper** - Displays a animation of the iPaper flipping automaticaly between pages
* **Maxi spread** - Displays a stylized version of two conjoining pages from the iPaper.

For Flipbook folders, there are 2 kinds of minipapers:
* **Random stack** - Displays a random stack of iPapers, with the frontpage for each iPaper within the category
* **Cover flow** - Displays the frontpages of each iPaper wihtin the category lined up next to each other, with the ability to browser through them

Once integrated on your website, clicking a Minipaper will redirect the user to the actual Flipbook being displayed.

## Minipapers in responsive design

```html
<div style="position: relative; width: 100%; padding-bottom: 50%;">
    <iframe style="display: block; position: absolute; top:0; right: 0; bottom: 0; left: 0; width: 100%; height: 100%;" scrolling="no" frameborder="0" src="................"></iframe>
</div>
```

## Custom redirection

It is possible to override the target of redirection when a users clicks the iPaper. To achieve this, the HTML used for integration must be slightly modified, by appending a TargetUrl query parameter to the src attribute of the iframe.


The Minipaper iframe HTML code has a src attribute that specifies the location of the iPaper. To specify custom redirection, ```&TargetUrl=[URL]``` must be appended at the end of the ```src``` value, where ```[URL]``` is replaced for an actual URL. The specified URL must be fully qualified, starting with ```http://``` (or ```https://```), and must also be URL-encoded. There are several online tools for encoding text to URL-format; here's one of them: [http://meyerweb.com/eric/tools/dencoder/](http://meyerweb.com/eric/tools/dencoder/)

### Example

If you want your Minipaper to redirect to [http://google.com](http://google.com), the ```TargetUrl``` parameter should be: ```&TargetUrl=http%3A%2F%2Fgoogle.com```
And in the context of the iframe code, the result would be:

```html
<iframe style="width:220px; height:160px" src="http://wwww.example.com/MyPaper/MiniPaperFrame.aspx?PA=2&TargetUrl=http%3A%2F%2Fgoogle.com" allowtransparency="true" scrolling="no" frameborder="0"></iframe>
```
