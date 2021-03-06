---
title: ScannerName element
description: The required ScannerName element specifies the administratively assigned user-friendly name of the scanner.
ms.assetid: 013a1cb8-4b59-4271-a7bd-eb8d741643e5
keywords: ["ScannerName element Imaging Devices"]
topic_type:
- apiref
api_name:
- wscn ScannerName xml lang "..."
api_type:
- Schema
ms.author: windowsdriverdev
ms.date: 11/28/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# ScannerName element


The required **ScannerName** element specifies the administratively assigned user-friendly name of the scanner.

Usage
-----

``` syntax
<wscn:ScannerName xml:lang="..."
  lang = "xs:string">
  text
</wscn:ScannerName xml:lang="...">
```

Attributes
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>lang</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>No</p></td>
<td><p></p>
<p>(Optional) A character string that identifies the languages of the string that string specifies.<em>string</em></p></td>
</tr>
</tbody>
</table>

Text value
----------

A character string that specifies the scanner's user-friendly name.

## Child elements


There are no child elements.

## Parent elements


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>Element</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[<strong>ScannerDescription</strong>](scannerdescription.md)</p></td>
</tr>
</tbody>
</table>

Remarks
-------

The configuration of the **ScannerName** element's value is implementation-specific; for example, you can configure this value through the scanner's local console or the device's web server. If a device has only one hosted service, its friendly name and **ScannerName** element should have the same value. If the device contains several hosted services, **ScannerName** should identify the scanner.

A scan device can return multiple versions of this element to enable support for multiple localized languages by using the **xml:lang** attribute.

Examples
--------

The following code example shows how you can use the ScannerName element.

```
<wscn:ScannerName xml:lang="en-AU, en-CA, en-GB, en-US">
  Accounting Scanner in Copy Room 2
</wscn:ScannerName>
```

## <span id="see_also"></span>See also


[**ScannerDescription**](scannerdescription.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bimage\image%5D:%20ScannerName%20element%20%20RELEASE:%20%2811/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")





