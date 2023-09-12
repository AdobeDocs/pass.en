---
description: You can use TVSDK to send arbitrary data in cookie headers for session management, gate access, and so on.
title: Work with cookies
exl-id: 7f0e7d77-0718-4df7-8380-0e9351f588bc
---
# Work with cookies {#work-with-cookies}

You can use TVSDK to send arbitrary data in cookie headers for session management, gate access, and so on.

Here is a sample request to the key server with some authentication:

1. Your customer logs in to your website in a browser and their login shows that this customer is allowed to view content. 
1. Based on what is expected by the license server, your application generates an authentication token.

   This value is passed to TVSDK. 
1. TVSDK sets this value in the cookie header. 
1. When TVSDK makes a request to the key server to get a key to decrypt the content, the request contains the authentication value in the cookie header.

   The key server knows that the request is valid.

To work with cookies: 

1. Create a `cookieManager` and add your cookies for the URIs to your cookieStore.

   For example: 

   ```java
   CookieManager cookieManager=new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   >[!TIP]
   >
   >When 302 redirect is enabled, the ad request may be redirected to a domain that is different from the domain to which the cookie belongs.

   TVSDK queries this `cookieManager` at runtime, checks whether there are any cookies associated with the URL, and automatically uses those cookies.

    If the cookies need to be updated in the application during playback, do not use `networkConfiguration.setCookieHeaders` API as the update will happen in JAVA cookie store.

    `networkConfiguration.setCookieHeaders` API sets the cookies to TVSDK's C++ CookieStore.

    When using JAVA cookies and sharing them between Application and TVSDK, use JAVA CookieStore to manage the cookies solely.

    Before playback is initialized, set the cookies to CookieStore using Cookie Manager as stated above.

    The cookie stored in CookieStore will be automatically picked up by TVSDK.

    If a cookie value needs to be updated later during playback, call the same add method of CookieStore with the same key and a new value field.

    Also set 
    `networkConfiguration.setReadSetCookieHeader`(false)
    before calling
    `config.setNetworkConfiguration(networkConfiguration)`

    >[!NOTE]
    >
    >After setting this 'setReadSetCookieHeader' to false, set the cookies for the key requests using JAVA cookie manager.

    `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
    This callback API will be fired whenever there is an update in C++ cookies (cookies which come from http response). Application needs to listen to this callback and can update their JAVA CookieStore accordingly so that their Network calls in JAVA can utilize the cookies as below:

    ```
    private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener() {
    @Override
    public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) {
    List<HttpCookie> cookies = cookiesUpdatedEvent.getHttpCookies();
    for(int i = 0; i < cookies.size(); i++)
    { HttpCookie c = cookies.get(i); // To set this cookie on to the cookie store //c.setValue("newValue"); //If you want to modify the value of the cookie URI myuri = URI.create(cookiesUpdatedEvent.getDomainString()); cookieManager.getCookieStore().add(myuri,c); }
    }
    }
    ```
