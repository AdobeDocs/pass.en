---
title: Header - AP-Partner-Framework-Status
description: REST API V2 - Header - AP-Partner-Framework-Status
---

# Header - AP-Partner-Framework-Status {#header-ap-partner-framework-status}

>[!NOTE]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Overview {#overview}

The <b>AP-Partner-Framework-Status</b> request header contains status information obtained from a partner framework in order to achieve single sign-on (SSO).

## Syntax {#syntax}

<table>
   <tr>
      <td style="background-color: #DEEBFF;" colspan="2"><b>AP-Partner-Framework-Status</b>: &lt;partner_framework_status_information&gt;</td>
   </tr>
   <tr>
      <td>Header Type</td>
      <td>Request header</td>
   </tr>
   <tr>
      <td>Standard</td>
      <td>No</td>
   </tr>
</table>

## Directives {#directives}

<b>&lt;partner_framework_status_information&gt;</b>

The `Base64-encoded` value of the JSON element containing the following attributes:

<table>
   <tr>
      <th style="background-color: #EFF2F7; width: 15%;">Attribute</th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td>frameworkPermissionInfo</td>
      <td>
         This is a required attribute.
         <br/><br/>
         The user permissions status information returned by the partner framework and processed by the application.
         <br/><br/>
         This is a JSON element with the following attributes:
         <br/>
         <table>
            <tr>
               <th style="background-color: #EFF2F7; width: 15%;">Attribute</th>
               <th style="background-color: #EFF2F7;"></th>
            </tr>
            <tr>
               <td>accessStatus</td>
               <td>
                  This is a required attribute.
                  <br/><br/>
                  This is an enumeration with the following possible values:
                  <br/>
                  <ul>
                     <li>granted - The user allowed the application to access subscription information.</li>
                     <li>denied - The user denied the application to access subscription information.</li>
                     <li>pending - The user did not choose yet to allow the application to access subscription information.</li>
                     <li>notDetermined - The application is not allowed to access subscription information.</li>
                  </ul>
               </td>
            </tr>
            <tr>
               <td>error</td>
               <td>
                  This is an optional attribute.
                  <br/><br/>
                  This can be used to pass the partner framework error in case one is triggered while querying for user permissions status information.
                  <br/><br/>
                  This is a JSON element with the following attributes:
                  <br/>
                  <table>
                     <tr>
                        <th style="background-color: #EFF2F7; width: 15%;">Attribute</th>
                        <th style="background-color: #EFF2F7;"></th>
                     </tr>
                     <tr>
                        <td>code</td>
                        <td>A string that uniquely identifies the error as defined by partner framework.</td>
                     </tr>
                     <tr>
                        <td>message</td>
                        <td>A string that contains the description of the error as defined by partner framework.</td>
                     </tr>
                  </table>
               </td>
            </tr>
         </table>
      </td>
   </tr>
   <tr>
      <td>frameworkProviderInfo</td>
      <td>
         This is a required attribute.
         <br/><br/>
         The provider login status information returned by the partner framework and processed by the application.
         <br/><br/>
         This is a JSON element with the following attributes:
         <br/>
         <table>
            <tr>
               <th style="background-color: #EFF2F7; width: 15%;">Attribute</th>
               <th style="background-color: #EFF2F7;"></th>
            </tr>
            <tr>
               <td>id</td>
               <td>
                  This is a required attribute.
                  <br/><br/>
                  This is the mappingId which identifies the MVPD used during the authentication flow at the partner framework level.
               </td>
            </tr>
            <tr>
               <td>expirationDate</td>
               <td>
                  This is a required attribute.
                  <br/><br/>
                  This is the expiration date of the authenticated user profile, in case the user has successfully logged using a supported MVPD at the partner framework level.
               </td>
            </tr>
            <tr>
               <td>error</td>
               <td>
                  This is an optional attribute.
                  <br/><br/>
                  This can be used to pass the partner framework error in case one is triggered while querying for provider login status information.
                  <br/><br/>
                  This is a JSON element with the following attributes:
                  <br/>
                  <table>
                     <tr>
                        <th style="background-color: #EFF2F7; width: 15%;">Attribute</th>
                        <th style="background-color: #EFF2F7;"></th>
                     </tr>
                     <tr>
                        <td>code</td>
                        <td>A string that uniquely identifies the error as defined by partner framework.</td>
                     </tr>
                     <tr>
                        <td>message</td>
                        <td>A string that contains the description of the error as defined by partner framework.</td>
                     </tr>
                  </table>
               </td>
            </tr>
         </table>
      </td>
   </tr>
</table>

## Examples {#examples}

```JSON

// Partner framework status information
// {
//    "frameworkPermissionInfo": {
//        "accessStatus": "....",
//        "error": {
//            "code" : "....",
//            "message" : "...."
//        }
//     },
//    "frameworkProviderInfo" : {
//        "id" : "....",
//        "expirationDate" : "....",
//        "error" : {
//            "code" : "...",
//            "message" : "....."
//        }
//     }
// }  
 
// Base64-encoded
// ewogICAgImZyYW1ld29ya1Blcm1pc3Npb25JbmZvIjogewogICAgICAgICJhY2Nlc3NTdGF0dXMiOiAiLi4uLiIsCiAgICAgICAg
// ImVycm9yIjogewogICAgICAgICAgICAiY29kZSIgOiAiLi4uLiIsCiAgICAgICAgICAgICJtZXNzYWdlIiA6ICIuLi4uIgogICAg
// ICAgIH0KICAgIH0sCiAgICAiZnJhbWV3b3JrUHJvdmlkZXJJbmZvIiA6IHsKICAgICAgICAiaWQiIDogIi4uLi4iLAogICAgICAg
// ICJleHBpcmF0aW9uRGF0ZSIgOiAiLi4uLiIsCiAgICAgICAgImVycm9yIiA6IHsKICAgICAgICAgICAgImNvZGUiIDogIi4uLiIs
// CiAgICAgICAgICAgICJtZXNzYWdlIiA6ICIuLi4uLiIKICAgICAgICB9CiAgICB9Cn0gIA==
 
AP-Partner-Framework-Status: ewogICAgImZyYW1ld29ya1Blcm1pc3Npb25JbmZvIjogewogICAgICAgICJhY2Nlc3NTdGF0dXMiOiAiLi4uLiIsCiAgICAgICAgImVycm9yIjogewogICAgICAgICAgICAiY29kZSIgOiAiLi4uLiIsCiAgICAgICAgICAgICJtZXNzYWdlIiA6ICIuLi4uIgogICAgICAgIH0KICAgIH0sCiAgICAiZnJhbWV3b3JrUHJvdmlkZXJJbmZvIiA6IHsKICAgICAgICAiaWQiIDogIi4uLi4iLAogICAgICAgICJleHBpcmF0aW9uRGF0ZSIgOiAiLi4uLiIsCiAgICAgICAgImVycm9yIiA6IHsKICAgICAgICAgICAgImNvZGUiIDogIi4uLiIsCiAgICAgICAgICAgICJtZXNzYWdlIiA6ICIuLi4uLiIKICAgICAgICB9CiAgICB9Cn0gIA==
```
