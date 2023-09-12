---
title: Configure Tomcat
description: Configure Tomcat
copied-description: yes
exl-id: 766b66dd-6070-4b0d-a860-a426fca05e56
---
# Configure Tomcat{#configure-tomcat}

On the Individualization server, modify Tomcat's [!DNL conf/server.xml] file to include additional information in the access log. You can use this information for reporting purposes. 

1. Locate the configuration for the `AccessLogValve` in [!DNL server.xml] and modify the pattern as shown here:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` will record the value of the `x-forwarded-for` header. If you use an Apache reverse proxy to forward requests to the Tomcat server, this header will contain the original client's IP address, whereas `%h` records the Apache server's IP address. `%{request-id}r` will record the request identifier, which corresponds to the request ID contained in the Individualization application log. 

1. Edit [!DNL conf/server.xml] and set the `unpackwars` property to false.

   For both the Individualization and Key Generation servers, it is a good idea to edit [!DNL conf/server.xml] and set the `unpackwars` property to `false`. Otherwise, when you update the WARs, you may have to clean out the unpacked WAR folders as well.

>[!NOTE]
>
>Future DRM clients will require you to enable and configure the CORS (Cross-Origin Resource Sharing) filter that is available for Tomcat. Currently, no DRM clients have this requirement.
