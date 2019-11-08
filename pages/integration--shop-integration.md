---
title: Shop Integration
permalink: /integration/shop-integration
redirect_from: "/display/DOC/Shop+Integration"
---

Using shop configuration it is possible to let the user add a number of items to the shopping basket in the catalog, after which the contents can be sent to a remote site for further processing. At this point, the remote site can handle registration, payment, etc.

## Setup

Once the shop configuration has been enabled, you can enable integration by selecting &ldquo;Integration&rdquo; as the primary checkout option. Once enabled, you will have to provide an export URL. This is the URL to which the shop contents are sent, when the user invokes the shop export function. Finally, you can choose whether to send the data in the current window, or open it in a new window.

## Export format

We include the name, description, price, product ID, and amount, as selected in the catalog. We also include the public-facing URL of the flipbook that sent the data in the payload&mdash;this can be useful to determine the origin flipbook of a shop export. Shop variants exported this way will have the same format. An example of a shop XML is as follow:

```xml
<shop flipbookcompleteurl="https://public/url/of/your/flipbook">
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

{% include note.html content="Even though the shop XML also exposes the `paper` attribute alongside with `flipbookcompleteurl`, we strongly encourage you to use the latter because the former does not include the full public URL of the flipbook." %}

## Loading the exported shop XML

The following is a complete sample of an aspx page that is able to receive and parse the shop XML. What is done with it afterwards is up to you. This sample simply prints the contents of the basket to the page.

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
