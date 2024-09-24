---
title: User Metadata Feature
description: User Metadata Feature
exl-id: 9fd68885-7b3a-4af0-a090-6f1f16efd2a1
---
# User Metadata {#user-metadata}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>
</br>

## Introduction {#intro}

The User Metadata feature enables Programmers to access different types of user-specific data maintained by MVPDs.  User metadata types include zip codes, parental ratings, user IDs, and more.  *User* metadata is an extension to the previously available *static* metadata (Authentication token TTL, Authorization token TTL, and Device ID).


User Metadata Key Points:

- Passed to the Programmer's application during the authentication and authorization flows
- Values are saved in the token
- Values can be normalized if different MVPDs provide data in different formats
- Some parameters can be encrypted using the Programmer's key (e.g. zip code), see [User Metadata Certificate for encryption](./user-metadata-certificate.md) for encryption certificate generation
- Specific values are made available by Adobe, via a configuration change

## Obtaining User Metadata {#obtaining}

User metadata is available to Programmers via the AccessEnabler `getMetadata()` function and via the `/usermetadata` endpoint in the Clientless API.  Please refer to the platform API documentation for details on using `getMetadata()` and its corresponding callback `setMetadataStatus()` (or for the endpoints and parameters used in the Clientless API).

Programmers get metadata by supplying a key for the type of metadata they want to obtain: `getMetadata(key)`.  

The metadata is returned as follows: `setMetadataStatus(key, encrypted, data)`:

| Parameter   | Type    | Description                                                                                                                                                                 |
| ----------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `key`       | String  | Specifies the type of metadata requested                                                                                                                                    |
| `encrypted` | Boolean | A boolean flag signifying whether the "value" is encrypted or not. If this is "true" then "value" will actually be a JSON Web Encrypted representation of the actual value. |
| `data`      | Object  | A JSON Object that contains the representation of the metadata                                                                                                              |

 

The structure of the data parameter, values vary between types:

| Key | Value type | Sample | Description |
| --- | --- | --- | --- |
| `zip` | JSON Array | \["77754", "12345"\] | Zip Code |
| `householdID` | JSON String | "1o7241p" | Household identifier. If the MVPD does not support subaccounts, this will be identical to `userID` |
| `maxRating` | JSON Object |  { MPAA: "NR", <br>  VCHIP: "X",  <br>  URL: "http://manage.my/parental" } | Maximum parental rating for the user |
| `userID` | JSON String | "1o7241p" | The user identifier. In the case in which an MVPD supports subaccounts, and the user is not the main account, `userID` will be different than `householdID`. |
| `channelID` | JSON Array | \["channel-1", "channel-2" \] | A list of channels a user is entitled to view |
| `is_hoh` | JSON String | "1" | A flag that identifies if a user is head of household |
| `encryptedZip` | JSON String | ""  | Comcast exposes the zip code encrypted |
| `typeID` | JSON String | Primary | A flag that identifies if the user account is primary/secondary account |
| `primaryOID` | JSON String | "uuidd1e19ec9-012c-124f-b520-acaf118d16a0" | Household identifier. If `typeID` is Primary, will contain the value of the `userID` |
| hba_status | Boolean | "true"  "false" | A boolean flag signifying whether Home-Based Authentication is enabled for a particular integration |
| allowMirroring | Boolean | "true"  "false" | Indicates whether screen mirroring is allowed for this device or not |

>[!NOTE]
>
> **Note:** If the data parameter is encrypted, as is usually the case for the **zip key**, then the representation of the metadata key will be a JSON String instead of an Array or an Object.


**Important:** The actual User Metadata available to a Programmer depends on what an MVPD makes available.  Legal agreements must be signed with MVPDs before sensitive user metadata (such as zipcode) is made available in the production environment.

</br>

  
| Name | Details | Requires encryption | Comments |
| --- | --- | --- | --- |
| User ID | As provided by the MVPD | No  | This is the value that is then hashed by Adobe and exposed in the media token and in the sendTrackingData() callback.<br><br>The hashing in this case was done for historical reasons<br><br>This ID could be a household ID or a sub-account ID. This is typically not specified, it's just the ID tied to the login that was used at the time (which can be a primary one or a sub-account) |
| Upstream User ID | Provided by the MVPD to be used only for Concurrency Monitoring flows | No  | This value is used when enforcing concurrency limits across MVPD and Programmer sites and apps. <br><br>The ID can contain concurrency monitoring policies as well<br><br>For most MVPDs this value is equal to the User ID |
| Household User ID | Provided by the MVPD to be used mostly for Parental Control flows | No  | ID that allows Programmers to understand Household vs. Sub-account usage.<br><br>It's sometimes used as a Parental Controls substitute if true ratings are not available (If the user was logged in with the household account they can watch, otherwise rated content would not be displayed)<br><br>There is a lot of variation across MVPDs for how this is represented - household user ID, head of household ID, head of household flag etc. |
| Head of Household | Flag signaling if the current account is head of household or not | No  | see above |
| Type ID / Primary ID | Household account identifiers | No  | AT&T specific indicators for head of household.<br><br>Type ID = Flag that identifies if the user account is primary/secondary account<br><br>Primary OID = Household identifier. If TypeID is Primary, will contain the value of the userID |
| Max Rating | The max allowed rating for the current account | No  | Allows Programmers to filter out content that is not suited for account.<br><br>Has MPAA or VCHIP ratings |
| Channel Line Up | List of channels available in the user's package | No  | Used to quickly allow/remove various channels from portals that aggregate multiple networks</br></br> *Please note that preflight authorization generally allows more flexiblity for this usecase and should be used instead* <br><br>The OLCA specification allows for this as an AttributeStatement in the AuthN response |
| HBA Status | Indicates if authentication has happened via HBA | No  |     |
| Zip Code | User's billing zip code | Yes | Used for Broadcasting or Sporting events<br><br>Can be also provided with the AuthZ resonse for fast updates<br><br>Sensitive data, needs MVPD legal agreements |
| Encrypted Zip Code | User's billing zip code (Comcast) | Yes | As above but encrypted by Comcast |
| Language | User language settings | No  | Used to display messages in accordance to the user's preferences |
| Allow Mirroring | Indicates whether screen mirroring is allowed for this device or not | No  |     |



## Available Metadata {#available_metadata}

The following table lays out the current state of user metadata in the Adobe Pass Authentication eco-system:

  
|     | **Legal**<br><br>**Agreement**<br><br>**Signed (zip only)** | **User ID**<br><br>**on AuthN** | **Zipcode**<br><br>**on AuthN/Z** | **Rating**<br><br>**on AuthN/Z** | **Household**<br><br>**ID on AuthN/Z** | **Channel ID on AuthN** | **Head of Household on AuthN** | **Type ID on AuthN** | **Primary OID on AuthN** | Language | Upstream UserID **on AuthN** | HBA Status | OnNet | inHome | Allow Mirroring on AuthZ | **Notes** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Formal Name** | n/a | `userID` | `zip` | `maxRating` | `householdID` | `channelID` | is_hoh | typeID | primaryOID | language | upstreamUserID | hba_status | onNet | inHome | allowMirroring | 1.  For AuthN - The OiosamlMetadataParser must be changed so that all parsers have this new attribute enabled <br>2.  For AuthZ - There is no generic way, because authorization implementation is MVPD-specific |
| **Encryption required** | n/a | **No** | **Yes** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** |     |
| **Sensitive** | n/a | **No** | **Yes** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** |     |     |
| **Adobe IdP** | **Yes** | **Yes** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes** | **Yes** | **Yes** | **Yes** | **No** | **Yes** | **No** | **No** | **No** | **No** | No legal agreement needed, can be enabled. |
| **Synacor** | **Yes** | **Yes** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes** | **Yes** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** | **Legal agreement not covering all the proxied MVPDs.**   <br>This is generic support for Synacor - possibly not rolled-up to all their MVPDs. |
| Dish | **No** | **Yes** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** | Shares the same list as all Synacor MVPDs, plus upstreamUserID. |
| Comcast | **No** | **Yes** | **No** | **Yes (AuthZ only)** | **Yes (AuthZ only)** | **No** | **No** | **No** | **No** | **No** | **Yes** | **Yes** | **No** | **No** | **No** |     |
| **AT&T** | **Yes** | **Yes** | **Yes (AuthN only)** | **No** | **Yes (AuthN only)** | **No** | **No** | **Yes** | **Yes** | **No** | **Yes** | **No** | **No** | **No** | **No** | Legal agreement signed. |
| **Cablevision** | **Yes** | **Yes** | **Yes (AuthN only)** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** | Legal agreement signed. |
| **HTC** | **No** | **Yes** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** |     |
| **Proxy Massilon** | **Yes** | **Yes** | **Yes (AuthN only)** | **No** | **Yes (AuthN only)** | **No** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** | Legal agreement signed. |
| **Proxy Clearleap** | **Yes** | **Yes** | **Yes (AuthN only)** | **Yes (AuthZ only)** | **No** | **No** | **No** | **No** | **No** | **Yes** | **Yes** | **No** | **No** | **No** | **No** | Legal agreement signed. |
| Rogers | **No** | **Yes** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** |     |
| RCN | **Yes** | **Yes** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes (AuthN only)** | **No** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** |     |
| Charter | **Yes** | **Yes** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes (AuthN only)** | **No** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** |     |
| Verizon | **No** | **Yes** | **Yes (AuthN only)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Yes** | **Yes** | **No** | **No** | **No** |     |
| Eastlink | **No** | **Yes** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** |     |
| Proxy GLDS | **No** | **Yes** | **Yes (AuthN only)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** |     |
| DTV | **Yes** | **Yes** | **Yes (AuthN only)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** |     |
| COX | **No** | **Yes** | **Yes (AuthN only)** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** |     |
| Cogeco | **No** | **Yes** | **Yes (AuthN only)** | **No** | **Yes (AuthN only)** | **No** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** |     |
| Videotron | **No** | **Yes** | **Yes (AuthN only)** | **No** | **Yes*** | **No** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** | Exposes householdID with the same value as userID |
| Spectrum | **Yes** | **Yes** | **Yes (AuthN only)** | **Yes (AuthN only)** | **Yes (AuthN only)** | **No** | **No** | **No** | **No** | **No** | **Yes** | **Yes** | **No** | **No** | **Yes** |     |
| **All Other**<br><br>**MVPDs** | **No** | **Yes** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **No** | **Yes** | **No** | **No** | **No** | **No** | **No legal agreement yet, sensitive metadata not available for Production.**  <br>For all MVPDs, the User ID is available with no extra work. |


The list of user metadata types will be expanded as new types are made available and added into the Adobe Pass Authentication system.

## Code Samples {#code_samples}

- [Code Sample 1](#code_sample1)
- [Code Sample 2 (Mock getMetadata)](#code_sample2)


### Code Sample 1 {#code_sample1}

```
    // Assuming a reference to the AccessEnabler has been previously obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if(status ==1) {
        // User is authenticated, request metadata
        ae.getMetadata("zip");
        ae.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if(encrypted) {
        // The metadata value is encrypted
        // Needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 

### Code Sample 2 (Mock getMetadata) {#code_sample2}

```
    // Assuming a reference to the AccessEnabler has been
    //   previously obtained and stored in the "ae" variable
     
    // Mock the getMetadata() method
    var aeMock = {
        getMetadata: function(key) {
          var data = null;
          // Set mock data based on the received key,
          // according to the format in the spec
          switch(key) {
            case 'zip': 
              data = [ "1235", "23456" ];
              break;
            case 'maxRating': 
              data = { "MPAA": "PG-13", "VCHIP": "TV-14" };
              break;
            default:
              break;
          }
          // Call the metadata status just like AccessEnabler does
          setMetadataStatus(key, false, data);
        }
     }
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
      if (status == 1) {
        // User is authenticated, request metadata using mock object
        aeMock.getMetadata("zip");
        aeMock.getMetadata("maxRating");
      } else {
        ...
      }
    }
     
    // Implement the  setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
      if (encrypted) {
        // The metadata value is encrypted, so it
        //   needs to be decrypted by the programmer
         data = decrypt(data);
      }
      alert(key + "=" + data);
    }
```
 
<!---

For details on your particular platform, or to gain some insight into how User Metadata is processed on the MVPD side, see the appropriate link in Related Information below.  

## Related Information {#related}

- ActionScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- JavaScript - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaData)
- iOS - [getMetadata()](#getMeta), [setMetadataStatus()](#setMetaStatus)
- Android - [getMetadata()](#getMetadata), [setMetadataStatus()](#setMetadaStatus)
- Clientless - [AuthN Metadata](#authn_metadata)
- [MVPD Integration Guide: User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
-->
