---
description: You must configure server properties to reflect your environment. You can do this using any of the following 
title: Apply properties to server environments
exl-id: 0c78011a-e8c8-43a8-8c2d-a5c4ed54a8d7
---
# Apply properties to server environments{#apply-properties-to-server-environments}

You must configure server properties to reflect your environment. You can do this using any of the following:

* [!DNL flashaccess-i15n.properties] - Samples included in each of the [!DNL .war] files 

* [!DNL AdobeInitial.properties] - Sample located in the [!DNL /shared] folder on the DVD

  You can use this file to override the properties set in the WAR file as follows:

    1. Set the overriding property values in [!DNL AdobeInitial.properties] 
    1. Place [!DNL AdobeInitial.properties] on the classpath.

  >[!NOTE]
  >
  >Adobe recommends that you make use of the [!DNL AdobeInitial.properties] file, since this allows you to update your application WAR files without risking the loss of any previous property configuration setup you may have done in the [!DNL flashaccess-i15n.properties] file.

* The Java System property mechanism.

You can apply individual properties to these specific server environments:

* *Development* 
* *Staging* 
* *Production*

With this capability, you can use the same WAR file for all server environments. To apply properties to specific environments, append two underscore characters (' `__`') plus one of the following environment codes to the property *name*:

* `DEV` 
* `STAGE` 
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

For example, to set the log level to `INFO` for your production and staging servers, and to `DEBUG` for your development server: 

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

The server employs this search order for properties:

1. `propertyname_environment` in [!DNL AdobeInitial.properties] 

1. `propertyname_environment` in [!DNL flashaccess-15n.properties] 

1. `propertyname_environment` in Java System properties 
1. `propertyname` in [!DNL AdobeInitial.properties] 

1. `propertyname` in [!DNL flashaccess-15n.properties] 

1. `propertyname` in Java System properties

>[!NOTE]
>
>You must specify the server's environment name as a Java System property when starting the server. For example, when starting Tomcat with [!DNL catalina.bat], set the `CATALINA_OPTS` environment variable as follows:
>-DENVIRONMENT_NAME=[ DEV | STAGE | PROD ]
