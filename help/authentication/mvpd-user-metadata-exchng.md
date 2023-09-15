---
title: MVPD User Metadata Exchange
description: MVPD User Metadata Exchange
exl-id: 8bce6acc-cd33-476c-af5e-27eb2239cad1
---
# MVPD User Metadata Exchange

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#intro-user-metadata-exchange}

MVPDs maintain user-specific metadata about their customers that in some cases is shared with Programmers. The aim of Adobe Pass authentication is to broker an exchange of this "user metadata", but not to enforce any kind of rules regarding the exchange. The exchange rules are for MVPDs to work out with their Programmer partners. 

User metadata types available for exchange currently include the following:

* Zip code
* Maximum rating (VChip or MPAA)
* User ID
* Household ID
* Channel ID 

Using this feature, MVPDs and Programmers can implement special use cases such as parental control. For example, an MVPD can pass parental rating data to a Programmer, who then uses that data to filter available viewing choices for a user. 

User Metadata Key Points:

* The MVPD passes user metadata to the Programmer's application during the authentication and authorization flows
* Adobe Pass authentication saves the metadata values in the AuthN and AuthZ tokens
* Adobe Pass authentication can normalize values for MVPDs that provide user metadata in different formats
* Some parameters can be encrypted using the Programmer's key
* Specific values are made available by Adobe, via a configuration change
 
>[!NOTE]
>
>User metadata is an extension to the static metadata (Authentication token TTL, Authorization token TTL, and Device ID) previously available in Adobe Pass authentication.

## Examples {#example-mvpd-user-metadata-exch}

### Parental Control {#example-parental-control}

This example shows the exhange of the following:

*  [Programmer to MVPD Metadata Exchange](#progr-mvpd-metadata-exch)

*  [MVPD to Programmer Metadata Exchange Flow](#mvpd-progr-exchange-flow)

### Programmer to MVPD Metadata Exchange {#progr-mvpd-metadata-exch}

Currently the Programmer API, Adobe Pass authentication, and MVPD Authorizers all support only channel-level authorization. The channel is specified as a plain text string in the Programmer's getAuthorization() API call. This string is propagated all the way to the MVPD's authorizing backend:

From the Programmer's app or site, the user chooses an XACML capable MVPD (in this example, "TNT"). For information on XACML, see [eXtensible Access Control Markup Language](https://en.wikipedia.org/wiki/XACML){target=_blank}.
The Programmer's app forms an AuthZ request that includes the resource and its metadata.  This example includes an MPAA rating of "pg" in the media attribute of the channel element:

```XML
var resource = '<rss version="2.0" xmlns:media="http://video.search.yahoo.com/mrss/">
                    <channel> 
                        <title>TNT</title> 
                        <media:rating scheme="urn:mpaa">pg</media:rating>
                    </channel>
                </rss>';
getAuthorization(resource);
```

Adobe Pass authentication actually supports more granular authorization, down to the asset level, when supported by both the MVPD and the Programmer. The resource and its metadata are opaque to Adobe; the intent is to establish a standard format for specifying the resource ID and metadata in a normalized way, to send resource IDs to different MVPDs. 

>[!NOTE]
>
>If the user chooses a channel-only capable MVPD, then Adobe Pass authentication extracts ONLY the channel title ("TNT" in the example above) and passes only the title to the MVPD. 

### MVPD to Programmer Metadata Exchange Flow {#mvpd-progr-exchange-flow}

Adobe Pass authentication makes the following assumptions:

* The MVPD sends the max rating as part of the SAML response
* This information is saved as part of the authentication token
* An API is provided by Adobe Pass authentication to enable Programmers to retrieve this information
* Programmers implement this feature on their site or app (for example, to hide videos that are over the max rating for the user)

```XML
<saml:Assertion ID="pfxec5f92e0-8589-3fc3-c708-f4fb8e2fad59"
                 IssueInstant="2010-07-20T10:05:41Z" Version="2.0"
                 xmlns:xs="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:AttributeStatement>
        <saml:Attribute
                Name="MaxTVRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">tv-ma</saml:AttributeValue>
        </saml:Attribute>
        <saml:Attribute
                Name="MaxMovieRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">nc-17</saml:AttributeValue>
        </saml:Attribute>
    </saml:AttributeStatement>
</saml:Assertion>
```

### Notes {#notes-mvpd-progr-metadata-exch-flow}

**Resource Normalization and Validation.** Resource IDs can be passed as a plain string or an MRSS string. A Programmer can decide to use either the plain string format or the MRSS, but will need a prior agreement with the MVPD so that the MVPD knows how to treat that resource. 

**Resource ID and Metadata Specification.** Adobe Pass authentication uses the RSS standard with the Media RSS extension to specify a resource and its metadata. In conjunction with the Media RSS extension, Adobe Pass authentication supports a wide variety of metadata, such as parental controls (via `<media:rating>`) or geolocation (`<media:location>`). 

Adobe Pass authentication can also support transparent conversion from the legacy channel string to the corresponding RSS resource for MVPDs that require RSS. In the other direction, Adobe Pass authentication supports conversion from RSS+MRSS to plain channel title, for channel-only MVPDs. 

**Adobe Pass authentication ensures full backwards compatibility with existing integrations.** That is, for Programmers using channel-level authentication, Adobe Pass authentication takes care to package the channel ID in the necessary format prior to sending it to an MVPD that understands that format. The reverse also applies: if a Programmer specifies all of its resources in a new format, Adobe Pass authentication translates the new format to a simple channel string if authorizing against an MVPD that only does channel level authorization. 

## User Metadata Use Cases {#user-metadata-use-cases}

Use cases are ever-changing and expanding as more MVPDs make legal arrangements and add functionality. The following are examples of what user metadata can be used for.

* [MVPD User ID](#mvpd-user-id)
* [Household ID](#household-user-id)
* [Zip Code](#zip-code)
* [Max Rating (Parental Control)](#max-rating-parental-control)
* [Channel Lineup](#channel-line-up)

### MVPD User ID {#mvpd-user-id}

* As provided by the MVPD
* Not the user's actual login information, as it is hashed by the MVPD
* Can be used to indicate problems with or for specific users
* Encrypted
* MVPD Support: All MVPDs

### Household User ID {#household-user-id}

* Allows for good metric information
* Encrypted
* MVPD Support: Some MVPDs

### Zip Code {#zip-code}

* The user's billing zip code
* Primarily used to enforce Sporting event freeze period rules
* Can be provided with the AuthZ response for fast updates
* MVPD Support: Some MVPDs

### Max Rating (Parental Control) {#max-rating-parental-control}

* AuthN initially, plus AuthZ refresh
* Filter content out of the UI
* MPAA or VChip ratings
* MVPD Support: Some MVPDs

### Channel Lineup {#channel-line-up}

* MVPDs can provide a list of channels that the user is entitled to view
* Allows for quick UI painting
* The OLCA specification allows for this as an AttributeStatement in the AuthN response
* Supporting MVPDs: Some MVPDs

<!--
>[!RELATEDINFORMATION]
>
>* [Proxy MVPD Web Service](/help/authentication/proxy-mvpd-webserv.md)
>* [Content Metadata Exhange](/help/authentication/mvpd-content-metadata-exchange.md)
>* [OLCA AuthN / AuthZ Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank}
>* [User Metadata (Programmer Integration Guide)](/help/authentication/user-metadata-feature.md)
-->
