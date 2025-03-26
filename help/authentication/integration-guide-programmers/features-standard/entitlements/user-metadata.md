---
title: User Metadata
description: User Metadata
exl-id: 9fd68885-7b3a-4af0-a090-6f1f16efd2a1
---
# User Metadata {#user-metadata}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

User metadata refers to user-specific [attributes](#attributes) (e.g., zip codes, parental ratings, user IDs, etc.) that are maintained by MVPDs and provided to Programmers through the Adobe Pass Authentication [REST API V2](#apis).

User metadata becomes available after the authentication flow completes, but certain metadata attributes may be updated during the authorization flow, depending on the MVPD and the specific metadata attribute in question.

User metadata can be used to enhance personalization for users, but might also be used for analytics. For example, a Programmer might use a user's zip code to deliver localized news or weather updates, or to enforce parental controls.

Adobe Pass Authentication normalizes user metadata values when MVPDs provide data in different formats. Also, for certain attributes (e.g., zip code), the values can be [encrypted](#encryption) using a Programmer's certificate.

Adobe Pass Authentication enables Programmers to review the user metadata made available in their MVPD integrations and [manage](#management) them through the [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication).

## User Metadata Attributes {#attributes}

The following table lists some of the user metadata attributes that are made available to Programmers:

| Key              | Type    | Sample                                                       | Requires encryption | Description                                                                        | Details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|------------------|---------|--------------------------------------------------------------|---------------------|------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `userID`         | String  | "1o7241p"                                                    | No                  | Account identifier.                                                                | The attribute value can be a household identifier or a sub-account identifier. The `userID` value will differ from the `householdID` if the MVPD supports sub-accounts and the current user is not the primary account holder.                                                                                                                                                                                                                                                                                                                   |
| `upstreamUserID` | String  | "1o7241p"                                                    | No                  | Account identifier for concurrency monitoring.                                     | The attribute value can be used to enforce concurrency limits across MVPD and Programmer sites and apps. The `upstreamUserID` value is the same as the `userID` value for most MVPDs.                                                                                                                                                                                                                                                                                                                                                            |
| `householdID`    | String  | "1o7241p"                                                    | No                  | Account identifier for parental control.                                           | The attribute value can be used to differentiate between household and sub-account usage. Sometimes it can be used as a parental control substitute if true ratings are not available, if the user was logged in with the household account, they can watch, otherwise, rated content would not be displayed. There is a lot of variation across MVPDs for how this is represented (e.g., household user ID, head of household ID, head of household flag, etc.), if the MVPD does not support sub-accounts, this will be identical to `userID`. |
| `primaryOID`     | String  | "uuidd1e19ec9-012c-124f-b520-acaf118d16a0"                   | No                  | Account identifier.                                                                | The attribute is specific to AT&T. The `primaryOID` value is the same as the `userID` value when the `typeID` value is set to "Primary".                                                                                                                                                                                                                                                                                                                                                                                                         |
| `typeID`         | String  | "Primary"                                                    | No                  | Attribute that indicates if current user is a primary or secondary account holder. | The attribute is specific to AT&T. The `primaryOID` value is the same as the `userID` value when the `typeID` value is set to "Primary".                                                                                                                                                                                                                                                                                                                                                                                                         |
| `is_hoh`         | String  | "1"                                                          | No                  | Attribute that indicates if current user is head of household or not.              | The attribute is specific to Synacor.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `hba_status`     | Boolean | "true"                                                       | No                  | Attribute that indicates if current user authenticated through HBA or not.         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `allowMirroring` | Boolean | "true"                                                       | No                  | Attribute that indicates if current device can mirror screen or not.               | The attribute is specific to Spectrum.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `zip`            | Array   | \["77754", "12345"\]                                         | Yes                 | User's zip code.                                                                   | The attribute value can be used to deliver localized news, weather updates or sporting events. The `zip` value represents sensitive data that needs legal agreements with the MVPD. When encrypted, the representation of the `zip` key will be a `String` instead of an `Array`.                                                                                                                                                                                                                                                                |
| `encryptedZip`   | String  | ""                                                           | Yes                 | User's encrypted zip code.                                                         | The attribute is specific to Comcast.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `channelID`      | Array   | \["channel-1", "channel-2"\]                                 | No                  | List of channels the user is entitled to view.                                     | The attribute value can be used to filter various channels from portals that aggregate multiple networks. Our recommendation is to use the [Preauthorize API](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) instead of this user metadata attribute to filter out channels that are not available to the user.                                                                                             |
| `maxRating`      | Object  | { MPAA: "NR", VCHIP: "X", URL: "http://manage.my/parental" } | No                  | Maximum parental rating for the current user.                                      | The attribute value can be used to filter content that is not suited for current user based on "MPAA" or "VCHIP" ratings.                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `language`       | String  | "English"                                                    | No                  | Language settings.                                                                 | The attribute value can be used to display messages in accordance to the user's language preferences.                                                                                                                                                                                                                                                                                                                                                                                                                                            |

The user metadata attributes made available to a Programmer depend on what an MVPD provides. The following table lists the attributes made available by various MVPDs:

|                         | **Legal Agreement Signed (zip only)** | **User ID on AuthN** | **Upstream User ID on AuthN** | **Household ID on AuthN/Z** | **Primary OID on AuthN** | **Type ID on AuthN** | **Head of Household on AuthN** | **HBA Status** | **Allow Mirroring on AuthZ** | **Zip code on AuthN/Z** | **Channel ID on AuthN** | **Rating on AuthN/Z** | **Language** | **onNet** | **inHome** | **Notes**                                                                                                                                 |
|-------------------------|---------------------------------------|----------------------|-------------------------------|-----------------------------|--------------------------|----------------------|--------------------------------|----------------|------------------------------|-------------------------|-------------------------|-----------------------|--------------|-----------|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **Formal Name**         | n/a                                   | `userID`             | `upstreamUserID`              | `householdID`               | `primaryOID`             | `typeID`             | `is_hoh`                       | `hba_status`   | `allowMirroring`             | `zip`                   | `channelID`             | `maxRating`           | `language`   | `onNet`   | `inHome`   |                                                                                                                                           |
| **Requires Encryption** | n/a                                   | **No**               | **No**                        | **No**                      | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes**                 | **No**                  | **No**                | **No**       | **No**    | **No**     |                                                                                                                                           |
| **Sensitive**           | n/a                                   | **No**               | **No**                        | **No**                      | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes**                 | **No**                  | **No**                | **No**       | **No**    | **No**     |                                                                                                                                           |
| Adobe IdP               | **Yes**                               | **Yes**              | **Yes**                       | **Yes (AuthN only)**        | **Yes**                  | **Yes**              | **Yes**                        | **No**         | **No**                       | **Yes (AuthN only)**    | **Yes**                 | **Yes (AuthN only)**  | **No**       | **No**    | **No**     | Legal agreement not needed.                                                                                                               |
| Synacor                 | **Yes**                               | **Yes**              | **Yes**                       | **Yes (AuthN only)**        | **No**                   | **No**               | **Yes**                        | **No**         | **No**                       | **Yes (AuthN only)**    | **Yes**                 | **Yes (AuthN only)**  | **No**       | **No**    | **No**     | Legal agreement not covering all the proxied MVPDs. This is generic support for Synacor and possibly not rolled-up to all of their MVPDs. |
| Dish                    | **No**                                | **Yes**              | **Yes**                       | **Yes (AuthN only)**        | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **Yes**                 | **Yes (AuthN only)**  | **No**       | **No**    | **No**     | It shares the same list as all Synacor MVPDs, plus `upstreamUserID`.                                                                      |
| Comcast                 | **No**                                | **Yes**              | **Yes**                       | **Yes (AuthZ only)**        | **No**                   | **No**               | **No**                         | **Yes**        | **No**                       | **No**                  | **No**                  | **Yes (AuthZ only)**  | **No**       | **No**    | **No**     |                                                                                                                                           |
| AT&T                    | **Yes**                               | **Yes**              | **Yes**                       | **Yes (AuthN only)**        | **Yes**                  | **Yes**              | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **No**                  | **No**                | **No**       | **No**    | **No**     | Legal agreement signed.                                                                                                                   |
| DTV                     | **Yes**                               | **Yes**              | **Yes**                       | **No**                      | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **No**                  | **No**                | **No**       | **No**    | **No**     |                                                                                                                                           |
| COX                     | **No**                                | **Yes**              | **Yes**                       | **No**                      | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **No**                  | **No**                | **No**       | **No**    | **No**     |                                                                                                                                           |
| Cablevision             | **Yes**                               | **Yes**              | **Yes**                       | **No**                      | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **Yes**                 | **No**                | **No**       | **No**    | **No**     | Legal agreement signed.                                                                                                                   |
| Spectrum                | **Yes**                               | **Yes**              | **Yes**                       | **Yes (AuthN only)**        | **No**                   | **No**               | **No**                         | **Yes**        | **Yes**                      | **Yes (AuthN only)**    | **No**                  | **Yes (AuthN only)**  | **No**       | **No**    | **No**     |                                                                                                                                           |
| Charter                 | **Yes**                               | **Yes**              | **Yes**                       | **Yes (AuthN only)**        | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **No**                  | **Yes (AuthN only)**  | **No**       | **No**    | **No**     |                                                                                                                                           |
| Verizon                 | **No**                                | **Yes**              | **Yes**                       | **No**                      | **No**                   | **No**               | **No**                         | **Yes**        | **No**                       | **Yes (AuthN only)**    | **No**                  | **No**                | **No**       | **No**    | **No**     |                                                                                                                                           |
| HTC                     | **No**                                | **Yes**              | **Yes**                       | **No**                      | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **No**                  | **Yes**                 | **No**                | **No**       | **No**    | **No**     |                                                                                                                                           |
| Rogers                  | **No**                                | **Yes**              | **Yes**                       | **No**                      | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **No**                  | **No**                  | **No**                | **No**       | **No**    | **No**     |                                                                                                                                           |
| RCN                     | **Yes**                               | **Yes**              | **Yes**                       | **Yes (AuthN only)**        | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **No**                  | **Yes (AuthN only)**  | **No**       | **No**    | **No**     |                                                                                                                                           |
| Eastlink                | **No**                                | **Yes**              | **Yes**                       | **Yes (AuthN only)**        | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **Yes**                 | **Yes (AuthN only)**  | **No**       | **No**    | **No**     |                                                                                                                                           |
| Cogeco                  | **No**                                | **Yes**              | **Yes**                       | **Yes (AuthN only)**        | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **No**                  | **No**                | **No**       | **No**    | **No**     |                                                                                                                                           |
| Videotron               | **No**                                | **Yes**              | **Yes**                       | **Yes***                    | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **No**                  | **No**                | **No**       | **No**    | **No**     | It exposes `householdID` with the same value as `userID`.                                                                                 |
| Proxy Massilon          | **Yes**                               | **Yes**              | **Yes**                       | **Yes (AuthN only)**        | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **No**                  | **No**                | **No**       | **No**    | **No**     | Legal agreement signed.                                                                                                                   |
| Proxy Clearleap         | **Yes**                               | **Yes**              | **Yes**                       | **No**                      | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **No**                  | **Yes (AuthZ only)**  | **Yes**      | **No**    | **No**     | Legal agreement signed.                                                                                                                   |
| Proxy GLDS              | **No**                                | **Yes**              | **Yes**                       | **No**                      | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **Yes (AuthN only)**    | **No**                  | **No**                | **No**       | **No**    | **No**     |                                                                                                                                           |
| Other MVPDs             | **No**                                | **Yes**              | **Yes**                       | **No**                      | **No**                   | **No**               | **No**                         | **No**         | **No**                       | **No**                  | **No**                  | **No**                | **No**       | **No**    | **No**     | No legal agreement yet, sensitive metadata not available for Production. For all MVPDs the `userID` is available with no extra work.      |

>[!IMPORTANT]
>
> Legal agreements must be signed with MVPDs before sensitive user metadata (e.g., zip code) is made available.

## User Metadata Encryption {#encryption}

To encrypt and decrypt user metadata attributes, the Programmer needs to generate a certificate (public/private key pair) and to [self-configure](#management) the certificate through [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication) or to share the public key with Adobe Pass Authentication representatives.

Follow the steps below to ensure that the certificate is generated and configured correctly:

1. Download and install the OpenSSL toolkit (http://www.openssl.org).

1. Generate a Certificate Signing Request (CSR):

   * Generate a key pair. On your command terminal run the following:

     ```bash
     openssl genrsa -des3 -out mycompany-license.key 2048
     ```

   * Generate the CSR. On your command terminal run the following:

     ```bash
     openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch
     ```

     You will be prompted to enter the password for the private key.

   * Create a back-up copy of your private key and password. Sample CSR:

      ```
      -----BEGIN CERTIFICATE REQUEST-----
      MIIBnTCCAQYCAQAwXTELMAkGA1UEBhMCU0cxETAPBgNVBAoTCE0yQ3J5cHRvMRIw
      EAYDVQQDEwlsb2NhbGhvc3QxJzAlBgkqhkiG9w0BCQEWGGFkbWluQHNlcnZlci5l
      eGFtcGxlLmRvbTCBnzANBgkqhkiG9w0BAQEFAAOBjQAwgYkCgYEAr1nYY1Qrll1r
      uB/FqlCRrr5nvupdIN+3wF7q915tvEQoc74bnu6b8IbbGRMhzdzmvQ4SzFfVEAuM
      MuTHeybPq5th7YDrTNizKKxOBnqE2KYuX9X22A1Kh49soJJFg6kPb9MUgiZBiMlv
      tb7K3CHfgw5WagWnLl8Lb+ccvKZZl+8CAwEAAaAAMA0GCSqGSIb3DQEBBAUAA4GB
      AHpoRp5YS55CZpy+wdigQEwjL/wSluvo+WjtpvP0YoBMJu4VMKeZi405R7o8oEwi
      PdlrrliKNknFmHKIaCKTLRcU59ScA6ADEIWUzqmUzP5Cs6jrSRo3NKfg1bd09D1K
      9rsQkRc9Urv9mRBIsredGnYECNeRaK5R1yzpOowninXC
      -----END CERTIFICATE REQUEST-----
      ```

1. Send the CSR to a Certificate Authority (CA) (for example, Verisign).

1. The CA will send you the certificate in .p7b format (PKCS#7, Cryptographic Message Syntax Standard).

1. Deploy the .p7b certificate. Convert the PKCS#7 (.p7b) file to a PKCS#12 (PFX file, Personal Information Exchange Syntax Standard) using your private key, and generate the PEM file (concatenated certificate container file):

   * Convert PKCS#7 file to a temporary PEM file. On your command line run the following:

      ```
      openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem -outform PEM -print_certs
      ```

   * Convert the temporary PEM file to a PFX file. On your command line run the following:

      ```
      openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password
      ```

   * Convert the temporary PEM file to a final PEM file. On your command line run the following:

      ```
      openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM
      ```

1. Use the PEM file to [configure](#management) the certificate through [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication) or send the PEM file to the Adobe Pass Authentication representatives.

   * Refer to the next section for more details on how to manage certificates through the [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication).

   * Adobe Pass Authentication supports both a primary and a backup certificate. If your primary certificate becomes compromised in any way, you can revoke it, and switch to the secondary certificate. This will ensure a smooth transition between certificates with minimal customer impact.

## User Metadata Management {#management}

>[!IMPORTANT]
>
> In case you do not have access to the Adobe Pass TVE Dashboard, create a ticket through our [Zendesk](https://adobeprimetime.zendesk.com) and ask your Technical Account Manager (TAM) to make the appropriate changes for you.

The Adobe Pass TVE Dashboard is a tool for Adobe Pass Authentication customers (Programmers) to manage their configuration and data. This self-service dashboard enables a range of functionalities that are described in the [Adobe Pass TVE Dashboard User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-overview.md) documentation.

To review and manage the user metadata attributes made available by an MVPD, follow the steps in the [TVE Dashboard User Guide for Integrations](/help/authentication/user-guide-tve-dashboard/tve-dashboard-integrations.md#user-metadata) documentation.

To review and manage the certificates used for encrypting user metadata attributes, follow the steps in the [TVE Dashboard User Guide for Programmers](/help/authentication/user-guide-tve-dashboard/tve-dashboard-programmers.md#certificates) or the [TVE Dashboard User Guide for Channels](/help/authentication/user-guide-tve-dashboard/tve-dashboard-channels.md#certificates) documents.  

## REST API V2 {#rest-api-v2}

The user metadata attributes can be retrieved using the following APIs:

* [Retrieve profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)
* [Retrieve profile for specific mvpd](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md)
* [Retrieve profile for specific code](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md)

Refer to the **Response** and **Samples** sections of the above APIs to understand the structure of the user metadata attributes.

>[!IMPORTANT]
>
> User metadata becomes available after the authentication flow completes, therefore the client application does not need to query a separate endpoint to retrieve the [user metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md) information, as it is already included in the profile information.

For more details about how and when to integrate the above APIs, refer to the following documents:

* [Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)
* [Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)

Certain metadata attributes may be updated during the authorization flow, depending on the MVPD and the specific metadata attribute. As a result, the client application may need to query the above APIs again to retrieve the latest user metadata.

>[!MORELIKETHIS]
>
> [Authentication Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authentication-phase-faqs-general)
