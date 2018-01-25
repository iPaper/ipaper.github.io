---
title: Shop Integration
permalink: /integration/shop-integration
redirect_from: "/display/DOC/Shop+Integration"
---

Using the Shop module it's possible to let the user add a number of items to the shopping basket in the catalog, after which the contents can be sent to a remote site. At this point, the remote site can handle registration, payment, etc.

## Setup

Once the Shop module has been enabled, you can enable integration by checking the "Enable Integration" checkbox under the Shop module settings. Once enabled, you will have to provide an export url. This is the url to which the shop contents are sent, when the user invokes the shop export function. Finally you can choose whether to send the data in the current window, or open it in a new window.

## Export Format

We include the name, description, price, product ID and amount, as selected in the catalog. We also include a reference to the Flipbook that sent the data - this can be useful to determine the origin Flipbook of a shop export. Shop variants exported this way will have the same format. Sample xml:

```xml
<shop paper="/Products/Cocacola/">
    <item>
        <amount>2</amount>
        <productid><![CDATA[AB123]]></productid>
        <price>99.95</price>
        <name><![CDATA[Coca cola]]></name>
        <description><![CDATA[Coca-Cola is a carbonated soft drink]]></description>
    </item>
    ...
</shop>
```

## Loading the Exported Shop XML

The following is a complete sample of an aspx page that's able to receive and parse the shop xml. What's done with it afterwards is up to you. This sample simply prints the contents of the basket to the page.

```cshtml
<%@ Page Language="C#" AutoEventWireup="true" ValidateRequest="false" %>
<%@ Import Namespace="System.Xml" %>
<%@ Import Namespace="System.Collections.Generic" %>
<%@ Import Namespace="System.Globalization" %>

<script runat="server">
    struct Item
    {
        public string ID;
        public int Amount;
        public decimal Price;
        public string Description;
        public string Name;
    }

    void Page_Load(object sender, EventArgs e)
    {
        if (!String.IsNullOrEmpty(Request.Form["basket"])) {

            var xd = new XmlDocument();
            xd.LoadXml(Request.Form["basket"]);

            var items = new List<Item>();
            foreach (XmlNode xn in xd.SelectNodes("//item"))
            {
                var item = new Item();
                item.Amount = Convert.ToInt32(xn.SelectSingleNode("amount").InnerText);
                item.ID = xn.SelectSingleNode("productid").InnerText;

                string price = xn.SelectSingleNode("price").InnerText;
                if (!String.IsNullOrEmpty(price))
                    item.Price = Convert.ToDecimal(price, new CultureInfo("en-US"));

                item.Description = xn.SelectSingleNode("description").InnerText;
                item.Name = xn.SelectSingleNode("name").InnerText;

                items.Add(item);
            }

            foreach (var item in items)
                Response.Write(String.Format(@"ID: {0}
                                                - Amount: {1}
                                                - Price: {2}
                                                - Description: {3}
                                                - Name: {4}", item.ID, item.Amount, item.Price, item.Description, item.Name));
        }
    }
</script>
```

## Returning Visitors

In some cases, you may want to identify a user coming back from a Flipbook, who originates from your website. By including a ```?Affiliate_Key=Value``` querystring parameter, you'll get the same parameter back when the shop is exported.

For example, if the export URL is set to "[http://google.com/](http://google.com/)" and you send the user to the catalog with the following address: "[http://url-to-catalog/?Affiliate_ShopID=25](http://url-to-catalog/?Affiliate_ShopID=25)", when the user then exports the basket, (s)he will then be sent to the following URL: "[http://google.com/?ShopID=25](http://google.com/?ShopID=25)".
