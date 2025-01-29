---
title: Protected Resources
description: Protected Resources
exl-id: 87f18ea7-4029-476a-a4a5-55bd14d9bf0c
---
# Protected Resources {#protected-resources}

>[!IMPORTANT]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

Protected resources represent content that users can stream and are identified by unique values established through agreements between MVPDs and participating Programmers.

Protected resources follow a hierarchical tree structure, with each level providing greater granularity for content authorization:

* Network
    * Channel
        * Show
            * Episode
                * Asset

## Protected Resources Identifiers {#identifiers}

The resource unique identifier can have two formats:

* A simple string format such as a unique identifier for a channel (brand).
* A media RSS (MRSS) format containing additional information such as the title, ratings and parental-control metadata.

In the case of a simple resource identifier, such as "REF30" (assumed to represent a channel), it can be translated into an RSS resource identifier as follows:

```RSS
    <rss version="2.0"> 
        <channel>
            <title>REF30</title>
        </channel>
    </rss>
```

In the case of a more complex resource identifier, the RSS resource identifier can include additional rating information as follows: 

```RSS
    <rss version="2.0" xmlns:media="http://search.yahoo.com/mrss/"> 
        <channel>
            <title>REF30</title>
            <media:rating scheme="urn:mpaa">pg</media:rating>
        </channel>
    </rss>
```

## REST API V2 {#rest-api-v2}

The Adobe Pass Authentication APIs retrieving preauthorization and authorization decisions require the client application to include the identifiers of protected resources as parameters.

The preauthorization and authorization decisions can be retrieved using the following APIs:

* [Retrieve preauthorization decisions using specific mvpd](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md)
* [Retrieve authorization decisions using specific mvpd](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md)

Refer to the **Request** and **Samples** sections of the above APIs to understand the required format for providing the unique identifiers of protected resources.

The unique identifiers are opaque to Adobe Pass Authentication, as they are passed directly to the MVPD. If the MVPD cannot recognize or parse a resource identifier, it returns an error to Adobe Pass Authentication, which then relays the error back to the client application using an [Enhanced Error Code](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md).

For more details about how and when to integrate the above APIs, refer to the following documents:

* [Basic preauthorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)
* [Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)
