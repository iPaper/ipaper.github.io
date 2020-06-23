---
title: Product Details View - Getting started
permalink: /integration/product-details-view-getting-started
redirect_from: "/display/DOC/product+details+view+getting+started"
tags: Flipbook integration
---
iPaper provides various options for adding shopping capabilities to your Flipbooks. In this document, we'll go into details on what the **Product Details View** enrichment is and what is required to get it working with your product data.

## The 'Product Details View' enrichment
The Product Details View enrichment type, is a link type which, when triggered from a flipbook, will look up product data on the internet and render product infomation inside the flipbook in a way that allows a user to see detailed informations about a product and ultimately buy the product.

For this to work, the link needs to know where to look for product data. That means that it needs an endpoint to call, and this endpoint should accept an `ID` value, so the endpoint can return data for the correct product.

## Features
The Product Details View supports different features which are all managed by the data returned from the product data endpoint.

### Currencies
If product prices are supplied in multiple currencies in the product data, we'll pull the price based on the Currency specified on the Flipbook. This allows the same product data to be consumed by Flipbooks targeting different countries/currencies.

### Call to action
The UI for a Product Details View link contains a call to action button which can have one of two actions:
- **OpenExternal**: Opens a new tab with the URL defined in the feed
- **AddToFlipbookCart**: Adds the product to Flipbook shopping cart

### Images
The Product Details View support multiple images, which will be show in a gallery if multiple images are returned in the product data.


## Endpoint
Your endpoint should accept a `GET` request, which will contain the product ID in either the path or the querystring.  

Here's a few examples of how a request to your endpoint could look:

- `https://api.your-domain.tld/data?productid=123456`
- `https://api.your-domain.tld/data/123456`
- `https://api.your-domain.tld/data/123456/json`
- `https://api.your-domain.tld/product/123456.json`

The next section describes how data should be formatted

### JSON format
When we contact your endpoint we expect data to be returned in the following JSON format:

```javascript
{
    "id": String, // ID / SKU of product
    "title": String, // Name or title of product
    "description": String, // Product description
    "prices": [ // An array of prices
        {
            "currency": String, // Name of currency. This should match what is set on the Flipbook. Typically it's a ISO 4217 Currency code (3 letters)
            "value": Number // Price in this specific currency
        }
    ],
    "cta": {
        "type": String, // Must be either "OpenExternal" or "AddToFlipbookCart"
        "uri": String // If "type" is "OpenExternal", "uri" should contain a full URI to the product 
    },
    "media": [ // An array of image. The order of images here, determines the order of images in the Flipbook
        {
            "type": "Image", // Required, must be "Image"
            "imageThumbnailUri": String, // Full URI to a thumbnail image
            "sourceUri": String // Full URI to a fullsize image
        }
    ]
}
```

> **Note**: It's important to note that the endpoint should return data for exactly one product.

## Security
To make sure your endpoint is safe, we're routing all requests for data through a small proxy layer.  
This allows us to hide your endpoint adress from users, so it's not visibile to any one but you.  
It also allows us to cache data for a short while, so even if a Flipbook gets a lot of trafic, requests to your data is throttled a bit.

## Limitations
We're constantly working on improving our products, so the limitations mentioned here might change over time. You can always [contact us](https://www.ipaper.io/contactlink) if you have any questions regarding a specific feature or limitation.

- We can only request data via a `GET` request. `POST` is current not possible
- We don't support Authentication headers of any kind
- It's not possible to configure our cache times


### JSON sample data
The section below contains different JSON samples that can serve as inspiration for what your endpoint should return.

#### Product with one price and one image and OpenExternal call to action
```javascript
{
    "id": "123456",
    "title": "My product name",
    "description": "My product description"
    "prices": [
        {
            "currency": "EUR",
            "value": 99.99
        }
    ],
    "cta": {
        "type": "OpenExternal",
        "uri": "https://domain.tld/product/123456"
    },
    "media": [
        {
            "type": "Image",
            "imageThumbnailUri": "https://domain.tld/images/thumb_123456.jpg"
            "sourceUri": "https://domain.tld/images/full_123456.jpg"
        }
    ]
}
```

#### Product with one price and one image and AddToFlipbookCart call to action
```javascript
{
    "id": "123456",
    "title": "My product name",
    "description": "My product description"
    "prices": [
        {
            "currency": "EUR",
            "value": 99.99
        }
    ],
    "cta": {
        "type": "AddToFlipbookCart"
    },
    "media": [
        {
            "type": "Image",
            "imageThumbnailUri": "https://domain.tld/images/thumb_123456.jpg"
            "sourceUri": "https://domain.tld/images/full_123456.jpg"
        }
    ]
}
```

#### Product with multiple prices and one image
```javascript
{
    "id": "123456",
    "title": "My product name",
    "description": "My product description"
    "prices": [
        {
            "currency": "EUR",
            "value": 99.99
        },
        {
            "currency": "USD",
            "value": 110.99
        }
    ],
    "cta": {
        "type": "AddToFlipbookCart"
    },
    "media": [
        {
            "type": "Image",
            "imageThumbnailUri": "https://domain.tld/images/thumb_123456.jpg"
            "sourceUri": "https://domain.tld/images/full_123456.jpg"
        }
    ]
}
```

#### Product with multiple prices and multiple images
```javascript
{
    "id": "123456",
    "title": "My product name",
    "description": "My product description"
    "prices": [
        {
            "currency": "EUR",
            "value": 99.99
        },
        {
            "currency": "USD",
            "value": 110.99
        }
    ],
    "cta": {
        "type": "AddToFlipbookCart"
    },
    "media": [
        {
            "type": "Image",
            "imageThumbnailUri": "https://domain.tld/images/thumb_123456_1.jpg"
            "sourceUri": "https://domain.tld/images/full_123456_1.jpg"
        },
        {
            "type": "Image",
            "imageThumbnailUri": "https://domain.tld/images/thumb_123456_2.jpg"
            "sourceUri": "https://domain.tld/images/full_123456_2.jpg"
        }
    ]
}
```