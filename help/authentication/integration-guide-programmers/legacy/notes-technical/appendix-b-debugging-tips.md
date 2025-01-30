---
title: Appendix B "Debugging Tips"
description: Appendix B "Debugging Tips"
exl-id: ea024797-315e-47c0-99ea-1ac49c8c9697
---
# (Legacy) Appendix B: Debugging Tips {#appendix-b-debugging-tips}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

## Clearing Temporary Data {#clearing-temporary-data}

Adobe Pass Authentication stores temporary data such as browser cache, LSOs cache and cookies. Clearing temporary data is important, to ensure that you get a clean slate when testing.

- [Clearing the Browser Cache and Cookies](#clearing-the-browser-cache-and-cookies)
- [Clearing LSOs Cache](#clearing-lsos-cache)  
  

## Clearing the Browser Cache and Cookies {#clearing-the-browser-cache-and-cookies}

It is browser dependable, but in Firefox:  "Tools" -\> "Clear Recent History…" -\> On "Time range to clear:" select "Everything"; and on "Details": check the "Cookies" and "Cache" -\> Click on "Clear Now".  
 

## Clearing LSOs Cache {#clearing-lsos-cache}

Access the [Flash Player help](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html).
  
Select the ```entitlement.\*``` (depending on what it is tested) and click "Delete website".  
 

## Debugging Tools {#tools}

Adobe Pass Authentication engineers use the following debugging tools:

- Firebug - <http://www.getfirebug.com/>
- Flashbug (works with the debug version of the flash player)
- Fiddler - <http://www.fiddler2.com/fiddler2/>
- Charles - <http://www.charlesproxy.com/>
- Wireshark - <http://www.wireshark.org/>
