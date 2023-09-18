---
title: Understanding User IDs
description: Understanding User IDs
exl-id: 813a8501-db72-4850-a387-c8db6120db80
---
# Understanding User IDs {#understanding-user-ids}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

Conceptually, each user who initiates an entitlement flow is associated with a single, unique User ID. However, through the course of an entitlement flow, that one User ID can be presented in different ways, depending upon which API you obtain the ID from.

The `sessionGUID` in the Short Media Token is the secure form of the User ID, which is available via the `sendTrackingData()` call. In all current integrations, this is a persistent GUID for the user across time and devices. The source of the GUID starts with the User ID from the authentication response coming from the MVPD. However, some MVPDs could change their mind in the future, and start sending a transient GUID. If a Programmer wants to ensure that the MVPD source User ID in the AuthN response is persistent, they should arrange for that in their agreements with MVPDs.

Here are the different ways the User ID is represented in the Adobe Pass Authentication APIs:

| Property | Purpose | Hashed | Digitally Signed | Description | 
| --- | --- | --- | --- | --- |
| sendTrackingData() GUID property | Tracking/analytics | Yes | No | - The MVPD User ID, hashed by Adobe. The User ID is not traceable back to the source to the MVPD. </br> </br> - This form of the ID is not digitally signed, so it is not secure for fraud prevention. However, it is good enough for analytics.  </br> </br> - This form of the User ID is provided client-side on all of the events that Adobe Pass Authentication generates in the AuthN/AuthZ flow.|
| Short Media Token's sessionGUID property | Fraud tracking of concurrent usage | Yes | Yes | - This is the same as the User ID via sendTrackingData(), however, this one is digitally signed to protect its integrity and is good enough to be used for fraud tracking. </br> </br> - It is intended to be processed on the server side after using our validator library, and can be analyzed for fraud patterns before releasing the video stream to the client.  Doing any of these tasks is up to the Programmer.| 
| getMetadata() userID property | Account linking, fraud investigation with MVPD | No | No | - This property allows Adobe to expose the actual source MVPD User ID to the Programmer. </br> </br> - In Adobe's configuration it can be set as encrypted or not (depending on the MVPD preference). If it's encrypted it will be encrypted with the public key from the Programmer's certificate provided to Adobe, so that it is not exposed in clear to the client. </br> </br> - This gives the Programmer the actual User ID from the MVPD, so it is something that can be used for account linking or fraud investigation directly with the MVPD.| 


**In conclusion**

*   In general, the MVPD provides a persistent unique ID <u>and passes it to Adobe on successful authentication</u>. It is generally consistent across all networks. The exception is Comcast MVPD, which provides a different User ID for each channel.

*   The MVPD User ID does not contain PII and it is NOT an account number. It does not need to be exposed in an encrypted form since we have validated with all the MVPDs that no PII is being sent.

How you use the User ID depends on the use case:

* If you need it for tracking/analytics, the most practical place is to get it from `sendTrackingData()`.
* If you need it on the server-side for stream release, fraud, or operational data, you can get it from the Media Token validator.
* If you need it for account linking and deeper fraud, check with your Adobe contact for availability.
