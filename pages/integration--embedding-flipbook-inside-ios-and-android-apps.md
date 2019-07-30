---
title: Embedding flipbooks inside iOS and Android App
permalink: /integration/embedding-flipbooks-inside-ios-and-android-apps
redirect_from: "/display/DOC/Embedding+iPapers+Inside+iOS+and+Android+Applications"
---

{% include important.html content="
	If you in any way exploit a quirk of our system to your benefit then we cannot guarantee that our flipbooks will continue to work as you would expect. If you feel the need to make any kind of workaround to achieve your desired behavior, make sure you validate it with us first. Otherwise you risk your app breaking at some point when we update our system.
	<br />
	<br />
	If you get in contact with us first, we'll do all we can to help you out and ensure a long term viable solution is made.
"%}

## Embedding the flipbook

iPaper will automatically detect which device is trying to access any given flipbook and display corresponding view. Whether that be the iPad, iPhone or Android views for handheld devices.

You should always link directly to a flipbook of the form:

```
http://partner.ipapercms.dk/Firma/Tilbudsavis/
```

{% include important.html content="It is very important that you never link directly to any files/subdirectories beneath the flipbook - only the main flipbook url can be trusted to be static."%}

## Important query string parameter when embedding the flipbook

For some mobile devices, we can't detect whether the navigation bar is present or not. As a result, content may either be shown too small, or cropped, in such cases.

To avoid this, you should hard code the browser height and send it to us in the query string like so:

```
http://partner.ipapercms.dk/Firma/tilbudsavis/?EmbeddedHeight=x
```

In the example above we will force our content to be exactly `x` pixels high, circumventing our normal size calculations.
{% include note.html content="Make sure that the EmbeddedHeight value is an integer with no decimals."%}
{% include important.html content="Unfortunately it is not possible to dynamically resize the embedded flipbook when using the EmbeddedHeight parameter. As such, you'll have to resize the container and reload the catalog with a new EmbeddedHeight value appended."%}

### Calculating the EmbeddedHeight value on iOS devices

On iOS, you can calculate the EmbeddedHeight value of a given UIWebView like this:

```c#
CGRect webViewSize = [_webView bounds];
int embeddedHeight = (int)webViewSize.size.height;
```

### Calculating the EmbeddedHeight value on Android devices

On Android you can calculate the EmbeddedHeight value of a given WebView like this:

```c#
CGRect webViewSize = [_webView bounds];
int embeddedHeight = (int)webViewSize.size.height;
```

## Shop Integration

When embedding a flipbook inside an iOS/Android application it is not possible to use our normal JavaScript API, as this requires the flipbook to be iframed. As an alternative it is possible to override the normal behavior of shop links and force them to open a specially formed URL, enabling you to intercept the call and thus be notified of users clicking on shop links.

To force the special shop link functionality, you'll have to add a special query string parameter to the flipbook URL. If the normal flipbook URL is this:

```
http://ipaper.ipapercms.dk/client/MyCustomFlipbook/
```

The embedded URL should be this, to invoke the special shop link handling:

```
http://ipaper.ipapercms.dk/client/MyCustomFlipbook/?ExternalJsonShopLinks=True
```

Once the `ExternalJsonShopLinks` parameter has been enabled, clicking on a shop link will then navigate the user to the following URL, containing a JSON object with all of the product details:

```
ipapershop://<payload>
```

| Property      | Type     | Description                                |
| ------------- | -------- | ------------------------------------------ |
| `title`       | `string` | Shop item title                            |
| `description` | `string` | Shop item description                      |
| `productId`   | `string` | Shop item product ID                       |
| `price`       | `number` | Shop item price                            |
| `originPage`  | `number` | Page number where the shop item is located |
| `quantity`    | `number` | Number of items added                      |
| `packageSize` | `number` | Number of items per package                |

An example of the emitted JSON is as follow:

```json
ipapershop: {
	title: "Milk",
	description: "Half gallon",
	productId: "M-926",
	price: 25.95,
	originPage: 4,
	quantity: 2,
	packageSize: 1
}
```

{% include note.html content="This functionality is only applicable to the mobile versions, and setting the `ExternalJsonShopLinks` parameter thus has no impact on the normal desktop version of the flipbook."%}

