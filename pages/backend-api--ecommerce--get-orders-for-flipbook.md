---
title: eCommerce.GetFlipbookOrdersByType
permalink: /backend-api/ecommerce/get-orders-for-flipbook
tags: Flipbook Backend API
---

## Description

Returns an XML document listing all orders completed over the last 3 months.

{% include note.html content="Only Enterprise+ licenses have access to this endpoint" %}

## Parameters
<table>
	<thead>
		<tr>
			<th>Name</th>
			<th>Values</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>paperId</td>
			<td>
				The paper id of the flipbook to return orders for		
			</td>
		</tr>
		<tr>
			<td>checkoutType</td>
			<td>
				The name of the checkout action that resulted in the orders.<br/>
				Parameter can be omitted to return orders of any origin.<br/>
				Supported checkout types:
				<ul>
					<li>CheckoutByEmail</li>
					<li>CheckoutBySharingEmail</li>
					<li>CheckoutByExport</li>
					<li>CheckoutByPrint</li>
					<li>CheckoutBySms</li>
					<li>CheckoutByWhatsApp</li>
				</ul>				
			</td>
		</tr>
	</tbody>
</table>

## Sample Response

```xml
<result>
	<code>
		<![CDATA[ SUCCESS ]]>
	</code>
	<message>
		<![CDATA[ Orders returned. ]]>
	</message>
	<data>
		<flipbooks>
			<flipbook id="1337" name="Sample Flipbook" url="/ipaper/sample-flipbook/">
				<orders count="1" earliestOrderDate="2020-06-25 11:57:35" latestOrderDate="2020-06-25 11:57:35">
					<order orderId="a1B2c3" orderDate="2020-06-25 11:57:35" checkoutType="CheckoutByEmail" orderLinesCount="2" totalOrderValue="5351,8">
						<orderLine>
							<productId>
								<![CDATA[ A123 ]]>
							</productId>
							<productName>
								<![CDATA[ Sample product 1 ]]>
							</productName>
							<productDescription>
								<![CDATA[ A description for Sample product 1 ]]>
							</productDescription>
							<productPrice>
								<![CDATA[ 1337,95 ]]>
							</productPrice>
							<amount>
								<![CDATA[ 2 ]]>
							</amount>
						</orderLine>
						<orderLine>
							<productId>
								<![CDATA[ A456 ]]>
							</productId>
							<productName>
								<![CDATA[ Sample product 2 ]]>
							</productName>
							<productDescription>
								<![CDATA[ A description for Sample product 2 ]]>
							</productDescription>
							<productPrice>
								<![CDATA[ 1337,95 ]]>
							</productPrice>
							<amount>
								<![CDATA[ 2 ]]>
							</amount>
						</orderLine>
					</order>
				</orders>
			</flipbook>
		</flipbooks>
	</data>
</result>
```

## Sample Error Response

If an invalid checkout type is sent the following error code will be returned.

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[UNSUPPORTED_CHECKOUT_TYPE]]></ code>
  <message><![CDATA[Checkout type is not supported]]></message>
  <data>
    <![CDATA[ Value of 'checkoutType' is not supported. Supported values: "", "CheckoutByEmail", "CheckoutByExport", "CheckoutByPrint", "CheckoutBySharingEmail", "CheckoutBySms", "CheckoutByWhatsApp" ]]>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
* READONLY
* LOGIN_SECURITY_VIOLATION
* UNSUPPORTED_CHECKOUT_TYPE