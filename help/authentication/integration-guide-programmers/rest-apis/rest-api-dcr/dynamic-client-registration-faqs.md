---
title: Dynamic Client Registration (DCR) FAQs
description: Dynamic Client Registration (DCR) FAQs
exl-id: 12268163-632e-4884-b35d-a29cc8ef45bf
---
# Dynamic Client Registration (DCR) FAQs {#rest-api-dcr-faqs}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This document provides high overview answers for frequently asked questions about the Adobe Pass Authentication Dynamic Client Registration (DCR) adoption.

For more information about the Dynamic Client Registration (DCR) overall, see the [Dynamic Client Registration Overview](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md) documentation.

>[!MORELIKETHIS]
>
> * [REST API v2 FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md)

## General FAQs {#general-faqs}

Start with this section if you are working on an application that needs to integrate the Dynamic Client Registration (DCR), whether it is a new application or an existing one that migrates from one of the previous mechanisms.

### Registration Phase FAQs {#registration-phase-faqs-general}

+++Registration Phase FAQs

#### 1. What's the purpose of the Registration Phase? {#registration-phase-faq1}

The purpose of the Registration Phase is to register the client application against Adobe Pass Authentication through the [Dynamic Client Registration (DCR)](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#dcr) process.

The Dynamic Client Registration (DCR) process requires the client application to obtain a pair of client credentials and retrieve an access token as the end goal of the Registration Phase.

For more information, refer to the [Dynamic Client Registration Overview](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md) documentation.

#### 2. Is the Registration Phase mandatory? {#registration-phase-faq2}

The Registration Phase is mandatory, but the client application can skip this phase if it has a cached pair of client credentials and an access token that are still valid.

#### 3. What's a software statement and how long is it valid? {#registration-phase-faq3}

The software statement is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#software-statement) documentation.

The software statement consists of a JSON Web Token (JWT) that can be generated and downloaded from the Adobe Pass [TVE Dashboard](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#tve-dashboard) by one of your organization administrators or by an Adobe Pass Authentication representative acting on your behalf.

The software statement is valid for an unlimited timeframe, but you may choose to ask an Adobe Pass Authentication representative to revoke it at any time.

The client application must store the software statement and use it when needing to retrieve client credentials.

For more details, refer to the [Dynamic Client Registration Overview](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md) documentation.

#### 4. How to generate and download a software statement? {#registration-phase-faq4}

This operation can be completed through the Adobe Pass [TVE Dashboard](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#tve-dashboard) by one of your organization administrators or by an Adobe Pass Authentication representative acting on your behalf.

For more details, refer to the [TVE Dashboard Channels User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-channels.md#registered-applications) or [TVE Dashboard Programmers User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-programmers.md#registered-applications) documentation.

#### 5. What happens if a software statement is revoked? {#registration-phase-faq5}

When the software statement is revoked, there is one important consequence to consider:

* The client applications using the revoked software statement will no longer be able to go through the [entitlement](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#entitlement) flows, meaning that users will get blocked from playing content.

#### 6. What are client credentials and how long are they valid? {#registration-phase-faq6}

The client credentials are a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#client-credentials) documentation.

The client credentials consist of a client identifier and client secret pair that can be retrieved from the Client Register endpoint.

The client credentials are valid for an unlimited timeframe.

The client application must store indefinitely the client credentials and use them when needing to retrieve an access token.

For more information, refer to the [Retrieve client credentials](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-client-credentials.md) documentation.

#### 7. How to manage client credentials? {#registration-phase-faq7}

We recommend the client application to manage a unique pair of client credentials for each user application instance in case of both client-to-server and server-to-server integrations with Adobe Pass Authentication.

The client application must store indefinitely the client credentials and use them when needing to retrieve an access token.

#### 8. What happens if cached client credentials are lost? {#registration-phase-faq8}

When cached client credentials are lost, there are three important consequences to consider:

* The client application must obtain a new pair of client credentials.
* The client application must obtain a new access token using the new pair of client credentials.
* The client application will need to ask the user to re-authenticate, as the client application will lose access to the authenticated profiles obtained before.

#### 9. What's an access token and how long is it valid? {#registration-phase-faq9}

The access token is a term defined in the [Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#access-token) documentation.

The access token consists of a [bearer token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-authorization.md) that can be retrieved from the Client Token endpoint.

The access token is valid for a limited and short timeframe specified at the moment of issue.

The client application must store the access token and use it until it expires when targeting REST API V2.

The client application must obtain a new access token before the current one expires to prevent unauthorized requests.

For more information, refer to the [Retrieve access token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md) documentation.

#### 10. How can the client application refresh an access token? {#registration-phase-faq10}

The client application must refresh an access token the same way as retrieving a new access token, but using cached client credentials.

The client application must not re-register to refresh an access token, instead it must use the stored client credentials, otherwise users would be required to re-authenticate.

For more information, refer to the [Retrieve access token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md) documentation.
