---
title: CMU API access
description: CMU API access
---
# Concurrency Monitoring Usage API access {#cmu-api-usage-access}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted. Contact your Adobe representative for availability questions.

## Access procedure overview {#api-access-procedure-overview}

We have updated CMU reports access to be compatible with OAuth 2.0 Dynamic Client Registration Protocol. A custom OAuth 2.0 authorization server is deployed to address the needs of Concurrency Monitoring application. \
In order for the Client applications to utilize the OAuth 2.0 authorization, the server must dynamically register to obtain specific information (client credentials) to be able to interact with it. As part of the registration process, the client must present a set of built-in metadata to the client registration endpoint.
This metadata is communicated as a software statement, which contains a "software_id" to allow our authorization server to correlate different instances of an application using the same software statement.
A software statement is a JSON Web Token (JWT) that asserts metadata values about the client software as a bundle. When presented to the authorization server as part of a client registration request, the software statement must be digitally signed or MACed using JSON Web Signature (JWS). \
You can find a more detailed explanation on what software statements are and how they work in the official documentation  <a href="https://datatracker.ietf.org/doc/html/rfc7591" target="_blank">[RFC7591]</a>.
Follow the steps in the sections below to gain access. 

## Access procedure steps {#access-procedure-steps}

1. Have a registered application in Adobe Pass DCR server. For this step please contact our [Support Team](mailto:tve-support@adobe.com).
2. Get the software statement
   1. Go to TVE Dashboard <a href="https://console-preprod.auth.adobe.com/#!/" target="_blank"> Pre-Prod </a>  or <a href="https://console.auth.adobe.com/" target="_blank">PROD</a>
   2. Select programmer
   3. Go to Applications tab
   4. Select application
   5. Click DownLoad Software Statement to get a file similar with bellow capture
      <figure>
          <img src="assets/software_statement_1_download.png"
               alt="Download Software Statement">
       </figure>
      <figure>
          <img src="assets/software_statement_2.png"
               alt="Software Statement Sample">
       </figure>
   
3. Obtain access token
   1. Get client credentials by using the software statement obtained above and performing the bellow call. In this way a client_id - client_secret pair will be obtained, that can be used to get the access token. 
      *This step should not be performed every time. It should be done again only when the credentials expire.*
      <figure>
          <img src="assets/dcr_request_1_get_client_credentials.png"
               alt="Get client credentials">
       </figure>
   
   2. Get access token by using the bellow call. Use this access token to call any CMU API until the token will expire.
      *This step should be performed only if the last generated token expired.*
      <figure>
          <img src="assets/dcr_get_access_token_call.png"
               alt="Get access token">
       </figure>
   
4. Call CMU API - see related information bellow. 
      <figure>
          <img src="assets/call_cmu_reports_sample.png"
               alt="Call CMU API">
       </figure>

## Related Information {#related-information}

* [CMU Overview](/help/concurrency-monitoring/cm-usage-reports.md)
* [CMU API](/help/concurrency-monitoring/cmu-api.md)
