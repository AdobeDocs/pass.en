---
title: How to make a privacy request
description: How to make a privacy request
exl-id: abb21306-98d6-4899-914a-bdfa85cbd204
---
# How to make a privacy request {#howto-make-privacy-request}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Identifiers and namespaces {#identifier-namespace}

When sending an Access or Delete Privacy request, the customer application needs to include the following identifiers:

* **mvpdID** - Unique identifier of the MVPD.
* **userID** - Uniquely identifies the user of a Programmer's app, but orginates from the MVPD. See Understanding User IDs in the Programmer Overview.
* **IMSOrgID** - he Adobe Experience Cloud Identity Management Service Organization ID, that uniquely idenfies the Customer in the Adobe Experience Cloud
        

Please check the sample below:

```JSON
"userIDs": [{
     "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",  -----> "Dish" is the id of the MVPD
     "type":"unregistered",
     "value":"1234-5678-8765-4321" ----> "1234-5678-8765-4321" is the userId associated with the MVPD account
}]

```

>[!IMPORTANT]
>
>Users must be authenticated to be able to generate privacy requests for Adobe Pass Authentication. Otherwise, programmers must find other means of extracting the MVPD userID.

## Types of requests {#req-type}

Adobe Pass Authentication supports Access and Delete requests.

### Access {#access-req}

For an Access request: 

we'll provide back a JSON file that contain a summary of total number of authentication and authorization requests created for that Data Subject.
all these events are filtered per Customer. 
 

**Request sample**

You must upload a JSON with the Adobe Pass Authentication identifiers for which you are submitting the data access request. To see what a well-formed JSON looks like, see this sample:

```JSON
{
    "companyContexts": [{
            "namespace": "imsOrgID",
            "value": "1234567890@AdobeOrg"
        }
    ],
    "users": [{
            "key": "John Dow",
            "action": ["access"],
            "userIDs": [{
                "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",
                "type":"unregistered",
                "value":"1234-5678-8765-4321"
             }]
         
        }
    ],
    
    "include":["primetimeAuthentication"],
    "regulation" : "ccpa"
}

```

**Response sample**

```JSON
{
    "jobId": "d9a6b417-f619-4420-82a3-09f61fa8eff3",
    "requestId": "15765127177927284RX-739",
    "userKey": "John Dow",
    "action": "access",
    "status": "complete",
    "submittedBy": "564f7c9a-e0c8-4e74-99b8-20317ae1e235@techacct.adobe.com",
    "createdDate": "12/16/2019 04:11 PM GMT",
    "lastModifiedDate": "12/16/2019 04:15 PM GMT",
    "userIds": [
        {
            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
            "value": "1234-5678-8765-4321",
            "type": "unregistered",
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Adobe Pass Authentication",
            "retryCount": 0,
            "processedDate": "12/16/2019 04:15 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "results": {
                    "userContexts": [
                        {
                            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
                            "namespaceId": 0,
                            "value": "1234-5678-8765-4321",
                            "type": "unregistered"
                        }
                    ],
                    "receiptData": {
                        "createdAt": "2019-12-16T16:15:23.4Z",
                        "message": "Data summary",
                        "numberOfAuthenticationSessions": "6",
                        "numberOfAuthorizationDecisions": "11"
                    }
                },
                "message": "Success"
            }
        }
    ],
    "downloadUrl": "https://va7gdprdevblob.blob.core.windows.net/va7gdprdevblobpublic/usa/4161962b9e8ef0027453d7cc02ecd93d/d9a6b417-f619-4420-82a3-09f61fa8eff3/d9a6b417-f619-4420-82a3-09f61fa8eff3.zip",
    "regulation": "ccpa"
}

```

### Delete {#delete-req}

You must upload a JSON with the Adobe Pass Authentication identifiers for which you are submitting the data delete request. To see what a well-formed JSON looks like, see this sample: 

**Request sample**

```JSON
{
    "companyContexts": [{
            "namespace": "imsOrgID",
            "value": "1234567890@AdobeOrg"
        }
    ],
    "users": [{
            "key": "John Dow",
            "action": ["delete"],
            "userIDs": [{
                "namespace":"http://www.adobe.com/primetimeAuthentication/Dish",
                "type":"unregistered",
                "value":"1234-5678-8765-4321"
             }]
         
        }
    ],
    
    "include":["primetimeAuthentication"],
    "regulation" : "ccpa"
}

```

**Response sample**

For a Delete request:

* we only share a receipt that the data was removed, not an aggregated file with all the data that was removed.
* the receipt included in the response contains a summary of total number of authentication and authorization tokens found for that Data Subject.

```JSON
{
    "jobId": "aab380d1-a0cd-4a0d-ba95-2649ee90c063",
    "requestId": "15759883098453100RX-074",
    "userKey": "John Dow",
    "action": "delete",
    "status": "complete",
    "submittedBy": "564f7c9a-e0c8-4e74-99b8-20317ae1e235@techacct.adobe.com",
    "createdDate": "12/10/2019 02:31 PM GMT",
    "lastModifiedDate": "12/10/2019 02:34 PM GMT",
    "userIds": [
        {
            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
            "value": "1234-5678-8765-4321",
            "type": "unregistered",
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Adobe Pass Authentication",
            "retryCount": 0,
            "processedDate": "12/10/2019 02:34 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "results": {
                    "userContexts": [
                        {
                            "namespace": "http://www.adobe.com/primetimeAuthentication/Dish",
                            "namespaceId": 0,
                            "value": "1234-5678-8765-4321",
                            "type": "unregistered"
                        }
                    ],
                    "receiptData": {
                        "createdAt": "2019-12-10T14:34:55.274Z",
                        "message": "Data summary",
                        "numberOfAuthenticationSessions": "2",
                        "numberOfAuthorizationDecisions": "3"
                    }
                },
                "message": "Success"
            }
        }
    ],
    "downloadUrl": "https://va7gdprdevblob.blob.core.windows.net/va7gdprdevblobpublic/usa/4161962b9e8ef0027453d7cc02ecd93d/aab380d1-a0cd-4a0d-ba95-2649ee90c063/aab380d1-a0cd-4a0d-ba95-2649ee90c063.zip",
    "regulation": "ccpa"
}

```

## How to trigger a request {#trigger-req}

There are 2 options for customers to send privacy requests to Adobe:

* **manually** - by using [Privacy Service User Interface](#privacy-service-ui)
* **automatically** - by using [Privacy Service API ](#privacy-service-api)

### By using Privacy Service UI {#privacy-service-ui}

A [complete tutorial](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=en#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) on how to access and use Privacy Service User Interface is available online through Adobe I/O services. Additionally, customers can use this link to access library of videos and articles on Privacy regulations. Click on the Adobe Experience Cloud and GDPR menu. This will open a number of videos - "GDPR UI How-to" explains how to use it.    

In the UI customers need to load their own IMSOrgID and a JSON containing GDPR requests details for each product. 

### By using Privacy Service API {#privacy-service-api}

Adobe Experience Platform Privacy Service provides a common, centralized facilitation of access/delete requests and opt-out-of-sale requests for private data.

The **Privacy Service API documentation** covers in-depth how an Adobe customer can integrate with Adobe API. 

**Visualize API calls with Postman (a free, third-party software):**

* [Privacy Service API Postman collection on GitHub](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Privacy%20Service%20API.postman_collection.json)
* [Video guide for creating the Postman environment](https://video.tv.adobe.com/v/28832)
* [Steps for importing environments and collections in Postman](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/)
 

**API paths:**

* PLATFORM Gateway URL: `https://platform.adobe.io/`
* Base path for this API: `/data/core/privacy/jobs`
* Example of a complete path: `https://platform.adobe.io/data/core/privacy/jobs/ping`
 

**Required headers:**

* All calls require the headers `Authorization`, `x-gw-ims-org-id`, and `x-api-key`. For more information on how to obtain these values, see the **authentication tutorial**.
* All requests with a payload in the request body (such as POST, PUT, and PATCH calls) must include the header `Content-Type` with a value of `application/json`.

<!--

>[!RELATEDINFORMATION]
>
>* [Privacy Services Overview](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?lang=en#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md)
>* Privacy Service API documentation

-->
