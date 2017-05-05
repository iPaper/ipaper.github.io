---
title: Paper.GetPaperStructure
permalink: /backend-api/paper/get-paper-structure
redirect_from: "/display/DOC/GetPaperStructure"
---

## Description

Returns an XML document listing all pages and page images for the requested PaperID.
{% include note.html content="You should not reference these urls from your own systems as they may change at any point. If you want to use the images, you should download them locally and host them yourself. We also may redirect the user to other domains, so they mustn't be references from Flash files directly, as crossdomain needs may change dynamically." %}


## Parameters

| Name               | Value
|--------------------|-------------------------------------------------------------
| paperID            | The ID of the iPaper whose structure should be returned
| includeIndexedText | If true, returns the text iPaper has indexed from each page

## Sample Response (Without Text)

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Paper structure retrieved.]]></message>
  <data>
    <paper id="1120" name="Dot_Matrix_Range" url="/demos/Dot_Matrix_range/">
      <pages>
        <page id="58367" number="1" part-of-index="False">
          <images>
            <image file-size="300" type="Zoom" url="http://flex.frontend.dk/demos/Dot_Matrix_range/Image.ashx?PageID=58367&amp;ImageType=Zoom" />
            <image file-size="90" type="Normal" url="http://flex.frontend.dk/demos/Dot_Matrix_range/Image.ashx?PageID=58367&amp;ImageType=Normal" />
            <image file-size="6" type="Thumb" url="http://flex.frontend.dk/demos/Dot_Matrix_range/Image.ashx?PageID=58367&amp;ImageType=Thumb" />
          </images>
        </page>
        ...
      </pages>
    </paper>
  </data>
</result>
```

## Sample Response (With Text)

```xml
<?xml version="1.0" encoding="utf-8"?>
<result>
  <code><![CDATA[SUCCESS]]></code>
  <message><![CDATA[Paper structure retrieved.]]></message>
  <data>
    <paper id="1120" name="Dot_Matrix_Range" url="/demos/Dot_Matrix_range/">
      <pages>
        <page id="58367" number="1" part-of-index="False">
          <text><![CDATA[Before Use 1. Safety precautions. 8 2. Before use . 13 Discs .15 Operation 1. About This Receiver . 18 Control Names and Operations.18 Panel Switches. 18 Turning the POWER ON or OFF .19 Switching Between the Audio and Navigation Screen .19 Turning the PND Display ON and OFF .20 Detaching the PND .20 Using the PND. 20 How to Detach the PND from the Main Unit. 20 Attaching the PND. 20 Using the Audio Cover.21 Using the Audio Cover . 21 Fitting the Audio Cover. 21 How to Detach the Audio Cover from the Main Unit. 21 Hands-Free Microphone and Light Sensor .21 Adjusting the Display Angle.22 Loading/Unloading a Disc .22 Loading Steps . 23 CD/DVD unloading steps . 24 Operation Conditions of this Receiver .25 2. Setup of This Receiver . 26 Setup of This Receiver.26 Calling the Setting screen .26 Enable guide tone . 26 Enable AUX. 26 Enable VTR . 27 Dim sub-display. 27 Link night view to headlights . 27 1]]></text>
          <images>
            <image file-size="300" type="1" url="http://flex.frontend.dk/demos/Dot_Matrix_range/Image.ashx?PageID=58367&amp;ImageType=Zoom" />
            <image file-size="90" type="2" url="http://flex.frontend.dk/demos/Dot_Matrix_range/Image.ashx?PageID=58367&amp;ImageType=Normal" />
            <image file-size="6" type="3" url="http://flex.frontend.dk/demos/Dot_Matrix_range/Image.ashx?PageID=58367&amp;ImageType=Thumb" />
          </images>
        </page>
        ...
      </pages>
    </paper>
  </data>
</result>
```

## Return Codes

* SUCCESS
* ERROR
