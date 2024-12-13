---
title: Using Charles Proxy
description: Using Charles Proxy
exl-id: bb38543f-f6bc-4b5a-91b8-41bc51ee4c56
---
# (Legacy) Using Charles Proxy {#using-charles-proxy}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

**Charles:** <http://charlesproxy.com>

 
## Download, Install and Get Started with Charles Proxy {#download-install-and-get-stared-with-charles-proxy}

- **Download** - <http://www.charlesproxy.com/download/>
- **Install** - <http://www.charlesproxy.com/documentation/installation/>
- **Getting Started** - <http://www.charlesproxy.com/documentation/getting-started/>

 
## Structure vs Sequence Tabs {#structure-vs-sequence-tabs}

There are two different ways to view the traffic:

1.  **Structure** - Requests are grouped by host
1.  **Sequence** - Requests are listed in the order they are called


## SSL and Certificates {#ssl-and-certificates}

Enable SSL Proxying `\[ *Proxy -\> Proxy Settings... -\> SSL* \]`

Check the "Enable SSL Proxying" checkbox and add all of the HTTPS locations.


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/ProxySettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/SSLSettings.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AddHttpsLocations.PNG)



- SSL Proxying - <http://www.charlesproxy.com/documentation/proxying/ssl-proxying/>
- SSL Certificates - <http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/> 
- SSL Proxying from Mobile devices - See below.

 
## Ignore / Exclude Hosts {#ignore-/-exclude-hosts}

If your output becomes too cluttered you can choose to ignore or exclude locations You can ignore or exclude locations by doing either of the following:

- Right-click on the requests you wish to ignore and then select "Ignore"
- Manually add the locations to exclude from `\[ *Proxy -\> Recording Settings... -\> Exclude* \]`

 
## DNS Spoofing {#dns-spoffing}

`\[ *Tools -\> DNS Spoofing...* \]`

 

DNS spoofing is very useful when trying to redirect a request to a different IP, especially when working with mobile devices:

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/DNSSpoofing.PNG)

<http://www.charlesproxy.com/documentation/tools/dns-spoofing/>

 
## Map Remote {#map-remote}

`\[ *Tools -\> Map Remote...* \]`

 

With map remote you can redirect an "incoming" request to a different endpoint. The most common use case for this feature is to "Map" `AccessEnabler.swf` to `AccessEnablerDebug.swf:`

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemote.PNG) ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/MapRemoteAdd.PNG)

<http://www.charlesproxy.com/documentation/tools/map-remote/>

 

## Reverse Proxy {#reverse-proxy}

<http://www.charlesproxy.com/documentation/proxying/reverse-proxy/>

## Mobile {#mobile}

### Use Charles on an iOS Device (iPhone / iPad) {#use-charles-on-an-ios-device-(iphone-/-ipad)}

#### SSL Connection from iPhone {#ssl-connection-from-iphone}

Browse to <http://charlesproxy.com/charles.crt> from your iOS device.  This will start the certificate install dialog:

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate1\(1\).PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate2\(1\).PNG)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceSSLCertificate3.PNG)

 </br>

Click `\[ *Install*... *Install*... *Done* \]` to complete installing the certificate.

<http://www.charlesproxy.com/documentation/faqs/ssl-connections-from-within-iphone-applications/>

 

#### Using Charles from an iOS device {#using-charles-from-an-ios-device}

On your iOS device select `\[ *Settings* -\> *Wi-FI* -\> (*YOUR\_WIFI\_NETWORK)* \]`. Click on the little blue arrow next to your network, and then go down to HTTP Proxy and select "Manual": 


 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy1.png)![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy2.PNG)


 </br>
Here you need to specify the IP and port of the machine where you are running Charles. <span style="line-height: 1.6em;">If you now open Safari on your iOS device and try to open a web page, you should get the following popup on the machine that's running Charles:
 
 </br>

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/iOSDeviceManualProxy3.PNG)

</br>
Click "Allow" to allow the device to use Charles to proxy all its
requests.

<http://www.charlesproxy.com/documentation/faqs/using-charles-from-an-iphone/>


#### iOS - Trust any certificates {#ios-trust-any-certificates}

<http://stackoverflow.com/questions/933331/how-to-use-nsurlconnection-to-connect-with-ssl-for-an-untrusted-cert>

#### iOS Authentication error - adobepass.ios.app cannot be found

<https://tve.zendesk.com/entries/22135907-ios-authentication-error-adobepass-ios-app-cannot-be-found>


## Use Charles for Android

<http://www.charlesproxy.com/documentation/configuration/browser-and-system-configuration>

  
Browse to [Charles proxy](http://charlesproxy.com/charles.crt) from your Android device.
