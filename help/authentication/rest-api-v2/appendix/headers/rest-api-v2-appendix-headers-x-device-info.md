---
title: Header - X-Device-Info
description: REST API V2 - Header - X-Device-Info
exl-id: 0ef25e06-86de-427a-a938-7ba3817f0d5e
---
# Header - X-Device-Info {#header-x-device-info}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

The <b>X-Device-Info</b> request header contains the client information (device, connection and application) related to the actual streaming device.

## Syntax {#syntax}

<table>
   <tr>
      <td style="background-color: #DEEBFF;" colspan="2"><b>X-Device-Info</b>: &lt;device_information&gt;</td>
   </tr>
   <tr>
      <td>Header Type</td>
      <td>Request header</td>
   </tr>
   <tr>
      <td>Standard</td>
      <td>No</td>
   </tr>
</table>

## Directives {#directives}

<b>&lt;device_information&gt;</b>

The `Base64-encoded` value of the JSON element containing at least the attributes marked as required by the following table. 

<table>
    <tr>
        <th style="background-color: #EFF2F7; width: 15%;">Key</th>
        <th style="background-color: #EFF2F7;">Description</th>    
        <th style="background-color: #EFF2F7; width: 15%;">Presence</th>
        <th style="background-color: #EFF2F7;">Possible Values</th>
    </tr>
    <tr>
        <td>primaryHardwareType</td>
        <td>The device’s primary hardware type.</td>
        <td></td>
        <td>
            The values are restricted:
            <ul>
                <li>Camera</li>
                <li>DataCollectionTerminal</li>
                <li>Desktop</li>
                <li>EmbeddedNetworkModule</li>
                <li>eReader</li>
                <li>GamesConsole</li>
                <li>GeolocationTracker</li>
                <li>Glasses</li>
                <li>MediaPlayer</li>
                <li>MobilePhone</li>
                <li>PaymentTerminal</li>
                <li>PluginModem</li>
                <li>SetTopBox</li>
                <li>TV</li>
                <li>Tablet</li>
                <li>WirelessHotspot</li>
                <li>Wristwatch</li>
                <li>Unknown</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>model</td>
        <td>The device’s model name.</td>
        <td><i>required</i></td>
        <td>e.g. iPhone, SM-G930V, AppleTV, etc.</td>
    </tr>
    <tr>
        <td>version</td>
        <td>The device’s version.</td>
        <td></td>
        <td>e.g. 2.0.1, etc.</td>
    </tr>
    <tr>
        <td>manufacturer</td>
        <td>The device’s manufacturing company/organization.</td>
        <td></td>
        <td>e.g. Samsung, LG, ZTE, Huawei, Motorola, Apple, etc.</td>
    </tr>
    <tr>
        <td>vendor</td>
        <td>The device’s selling company/organisation.</td>
        <td></td>
        <td>e.g. Apple, Samsung, LG, Google, etc.</td>
    </tr>
    <tr>
        <td>osName</td>
        <td>The device’s Operating System (OS) name.</td>
        <td><i>required</i></td>
        <td>
            The values are restricted:
            <ul>
                <li>Android</li>
                <li>Chrome OS</li>
                <li>Linux</li>
                <li>Mac OS</li>
                <li>OS X</li>
                <li>OpenBSD</li>
                <li>Roku OS</li>
                <li>Windows</li>
                <li>iOS</li>
                <li>tvOS</li>
                <li>webOS</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>osFamily</td>
        <td>The device’s Operating System (OS) group name.</td>
        <td></td>
        <td>
            The values are restricted:
            <ul>
                <li>Android</li>
                <li>BSD</li>
                <li>Linux</li>
                <li>PlayStation OS</li>
                <li>Roku OS</li>
                <li>Symbian</li>
                <li>Tizen</li>
                <li>Windows</li>
                <li>iOS</li>
                <li>tvOS</li>
                <li>macOS</li>
                <li>webOS</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>osVendor</td>
        <td>The device’s Operating System (OS) supplier.</td>
        <td></td>
        <td>
            The values are restricted:
            <ul>
                <li>Amazon</li>
                <li>Apple</li>
                <li>Google</li>
                <li>LG</li>
                <li>Microsoft</li>
                <li>Mozilla</li>
                <li>Nintendo</li>
                <li>Nokia</li>
                <li>Roku</li>
                <li>Samsung</li>
                <li>Sony</li>
                <li>Tizen Project</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>osVersion</td>
        <td>The device’s Operating System (OS) version.</td>
        <td></td>
        <td>e.g. 10.2, 9.0.1, etc.</td>
    </tr>
    <tr>
        <td>browserName</td>
        <td>The browser’s name.</td>
        <td></td>
        <td>
            The values are restricted:
            <ul>
                <li>Android Browser</li>
                <li>Chrome</li>
                <li>Edge</li>
                <li>Firefox</li>
                <li>Internet Explorer</li>
                <li>Opera</li>
                <li>Safari</li>
                <li>SeaMonkey</li>
                <li>Symbian Browser</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>browserVendor</td>
        <td>The browser’s building company/organisation.</td>
        <td></td>
        <td>
            The values are restricted:
            <ul>
                <li>Amazon</li>
                <li>Apple</li>
                <li>Google</li>
                <li>Microsoft</li>
                <li>Motorola</li>
                <li>Mozilla</li>
                <li>Netscape</li>
                <li>Nintendo</li>
                <li>Nokia</li>
                <li>Samsung</li>
                <li>Sony Ericsson</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>browserVersion</td>
        <td>The device’s browser version.</td>
        <td></td>
        <td>e.g. 60.0.3112</td>
    </tr>
    <tr>
        <td>userAgent</td>
        <td>The device’s user agent.</td>
        <td></td>
        <td>e.g. Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/602.4.8 (KHTML, like Gecko) Version/10.0.3 Safari/602.4.8</td>
    </tr>
    <tr>
        <td>displayWidth</td>
        <td>The device’s physical screen width.</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>displayHeight</td>
        <td>The device’s physical screen height.</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>displayPpi</td>
        <td>The device’s physical screen pixel density.</td>
        <td></td>
        <td>e.g. 294</td>
    </tr>
    <tr>
        <td>diagonalScreenSize</td>
        <td>The device’s physical screen diagonal dimension in inches.</td>
        <td></td>
        <td>e.g. 5.5, 10.1</td>
    </tr>
    <tr>
        <td>connectionIp</td>
        <td>The device’s IP used for sending HTTP requests.</td>
        <td></td>
        <td>e.g. 8.8.4.4</td>
    </tr>
    <tr>
        <td>connectionPort</td>
        <td>The device’s port used for sending HTTP requests.</td>
        <td></td>
        <td>e.g. 53124</td>
    </tr>
    <tr>
        <td>connectionType</td>
        <td>The network connection type.</td>
        <td></td>
        <td>e.g. WiFi, LAN, 3G, 4G, 5G</td>
    </tr>
    <tr>
        <td>connectionSecure</td>
        <td>The network connection security status.</td>
        <td></td>
        <td>
            The values are restricted:
            <ul>
                <li>true - in the case of a secure network</li>
                <li>false - in the case of a public hot spot</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>applicationId</td>
        <td>The application’s unique identifier.</td>
        <td></td>
        <td>e.g. CNN</td>
    </tr>
</table>


## Examples {#examples}

```JSON

// Device information
// {
//  "primaryHardwareType" : "MobilePhone",
//  "model":"SM-S901U",
//  "vendor":"samsung",
//  "version":"r0q",
//  "manufacturer":"samsung",
//  "osName":"Android",
//  "osVersion":"14"
// }
 
// BASE64-encoded
// ewogICJwcmltYXJ5SGFyZHdhcmVUeXBlIiA6ICJNb2JpbGVQaG9uZSIsCiAgIm1vZGVsIjoiU00tUzkwMVUiLAogICJ2ZW5kb3I
// iOiJzYW1zdW5nIiwKICAidmVyc2lvbiI6InIwcSIsCiAgIm1hbnVmYWN0dXJlciI6InNhbXN1bmciLAogICJvc05hbWUiOiJBbmRyb
// 2lkIiwKICAib3NWZXJzaW9uIjoiMTQiCn0=
 
X-Device-Info: ewogICJwcmltYXJ5SGFyZHdhcmVUeXBlIiA6ICJNb2JpbGVQaG9uZSIsCiAgIm1vZGVsIjoiU00tUzkwMVUiLAogICJ2ZW5kb3IiOiJzYW1zdW5nIiwKICAidmVyc2lvbiI6InIwcSIsCiAgIm1hbnVmYWN0dXJlciI6InNhbXN1bmciLAogICJvc05hbWUiOiJBbmRyb2lkIiwKICAib3NWZXJzaW9uIjoiMTQiCn0=
```
