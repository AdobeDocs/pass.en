---
title: Implementing the usage models overview
description: Implementing the usage models overview
copied-description: yes
exl-id: 48e7db54-484f-4c46-9a4e-a51bae7c84b4
---
# Implementing the usage models overview {#implementing-the-usage-models-overview}

The Reference Implementation includes business logic for demonstrating how to enable the following four different usage models for a piece of packaged content:

* Download-to-own (DTO) 
* Rental/Video-on-demand (VOD) 
* Subscription (all-you-can-eat) 
* Ad-funded

To enable the usage model demo, specify the custom property `RI_UsageModelDemo=true` at packaging time. If you are packaging content using the Media Packager command line tool, specify:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>If you do not activate the optional demo mode at packaging time, the license server uses the policy specified at packaging time to issue a license. If multiple policies were specified, the license server uses the first valid policy.

In the demo, the business logic on the server controls the actual attributes of the licenses generated. At packaging time, only minimal policy information must be included in the content. Specifically, the policy only needs to indicate whether authentication is required to access the content. To enable all four usage models, include one policy that allows anonymous access (for the Ad-funded model) and one policy that requires user name/password authentication (for the other 3 usage models). When requesting a license, a client application can determine whether to prompt the user for authentication based on the authentication information in the policies.

To control the usage model under which a particular user is to be issued a license, entries may be added to the Reference Implementation database. The `Customer` table contains user names and passwords for authenticating users. It also indicates whether the user has a subscription. Users with subscriptions will be issued licenses under the *Subscription* usage model. To grant a user access under the *Download to Own* or *Video on Demand* usage models, an entry may be added to the `CustomerAuthorization` table, which specifies each piece of content the user is allowed to access and the usage model. See the [!DNL PopulateSampleDB.sql] script for details on populating each table.

When a user requests a license, the Reference Implementation server checks the metadata sent by the client to determine if the content was packaged using the `RI_UsageModelDemo` property. If so, the following business rules are used:

* If one of the policies requires authentication:

    * If the request contains a valid authentication token, look for the user in the Customer database table. If the user was found:

        * If the `Customer.IsSubscriber` property is `true`, generate a license for the *Subscription* usage model and send it to the user. 
        
        * Look for a record in the `CustomerAuthorization` database table for this user and content ID. If a record was found:

            * If `CustomerAuthorization.UsageType` is `DTO`, generate a license for the *Download To Own* usage model and send it to the user. 
            
            * If `CustomerAuthorization.UsageType` is `VOD`, generate a license for the *Video On Demand* usage model and send it to the user.

    * If none of the policies allow anonymous access:

        * If there is not a valid authentication token in the request, return an "authentication required" error. 
        * Otherwise return a "not authorized" error.

* If one of the policies allows anonymous access, generate a license for the Ad-funded usage model and send it to the user.

Before the Reference Implementation server can issue licenses for the usage model demo, the server needs to be configured to specify how licenses are generated for each of the four usage models. This is done by specifying a policy for each usage model. The Reference Implementation includes four sample policies ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) or you may substitute your own policies. In [!DNL flashaccess-refimpl.properties], set the following properties to specify the policy to use for each usage model and place the policy files in the directory specified by the `config.resourcesDirectory` property:

```
# Policy file name for Download To Own usage  
RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol  
# Policy file name for Rental usage  
RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol  
# Policy file name for Subscription usage  
RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol  
# Policy file name for Ad Supported (free) usage  
RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
```
