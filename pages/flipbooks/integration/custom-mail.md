---
title: Custom Mail
permalink: /flipbooks/analytics/custom-mail
redirect_from: /integration/custom-mail
tags: Flipbook integration
---

## Configuration

Before custom mail can be setup in iPaper, you need to setup the SPF record on your domain first.

If you do not have an SPF record yet, you can add the following as a TXT record on the domain you wish for us to send of behalf of.

```
v=spf1 include:spf.ipaper.io ~all
```

In the case you already have an SPF record in your DNS configuration you should only add `include:spf.ipaper.io`, else you risk loosing emails that was previously configured via your SPF record.

{% include important.html content="Be aware if you already have an SPF record setup in your DNS, please do ensure you are only adding the partial record" %}

## Verification

To verify if the SPF record have been setup correctly you can use the following tool:

[https://mxtoolbox.com/SuperTool.aspx?action=spf%3aipaper.io&run=toolpage](https://mxtoolbox.com/SuperTool.aspx?action=spf%3aipaper.io&run=toolpage)

Replace "ipaper.io" with the desired domain.

If `spf.ipaper.io` appears in the list of results with a pass in `PrefixDesc` you should be all good.