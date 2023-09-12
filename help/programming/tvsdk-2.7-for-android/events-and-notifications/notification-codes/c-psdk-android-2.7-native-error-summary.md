---
title: Details for the NATIVE_ERROR notification
description: Details for the NATIVE_ERROR notification
copied-description: yes
exl-id: 51c75349-0fa8-405d-9e09-b51b425fe21b
---
# Details for the NATIVE_ERROR notification {#details-for-the-native-error-notification}

When TVSDK handles a native error, it returns some or all of the following metadata key values as strings.  

<table id="table_7F713B7A56024D8DA3C84E449D09CC91"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Metadata key name </th> 
   <th colname="col2" class="entry"> Metadata value </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR_CODE</span> </td> 
   <td colname="col2"> <p>Native error code from the AVE. </p> <p>These codes represent the following: 
     <ul id="ul_1F33D523DDFE4CE8B4F0DC279FF7E4F8"> 
      <li id="li_07A2D9BEE6364935A61EF3BD4AB6DE27">DRM errors (codes 3300 to 3367). These are the same as the equivalent Flash Player error codes </li> 
      <li id="li_433BA22DE3504AEEB623598BB4F939FA">Video playback errors (-1 to 89) </li> 
      <li id="li_B347CB151DB94DE0A1DDEB1B33D2DABA">Cryptography errors (300 to 307) </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_ERROR</span> </td> 
   <td colname="col2">Short description of the notification (for example, <span class="codeph"> AAXS_InvalidVoucher</span> or <span class="codeph"> DECODER_FAILED</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESCRIPTION</span> </td> 
   <td colname="col2"> Long description of the notification (for example, Ad resolving operation has failed). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR_CODE</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> numeric value as a string (for example, "13"). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> PSDK_ERROR</span> </td> 
   <td colname="col2"><span class="codeph"> com.adobe.mediacore.PSDKErrorCode</span> as a string (for example, <span class="codeph"> kECNetworkError</span>). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> WARNING</span> </td> 
   <td colname="col2"> Description of the warning. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> ERROR</span> </td> 
   <td colname="col2"> Description of the error. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>DRM</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="col2"> Minor error from the DRM module. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_STRING</span> </td> 
   <td colname="col2"> Description of the error. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DRM_ERROR_SERVER_URL</span> </td> 
   <td colname="col2"> URL of the DRM server to which TVSDK tried to talk. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Ad manifest load failure</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_URL</span> </td> 
   <td colname="col2"> URL of the content that failed to load. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_TYPE</span> </td> 
   <td colname="col2">Type of ad (a constant from the <span class="codeph"> MediaResource.Type</span> enum). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_DURATION</span> </td> 
   <td colname="col2"> Ad duration in milliseconds. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AD_ID</span> </td> 
   <td colname="col2"> ID assigned to the ad. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>File errors</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="col2"> Description of the error during media file download. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> URL</span> </td> 
   <td colname="col2"> URL of file being downloaded. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MANIFEST_ERROR</span> </td> 
   <td colname="col2"> Description of error during manifest file download. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="col2">Description of error during fragment (for example, <span class="codeph"> ts</span>) download. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Audio track errors</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_NAME</span> </td> 
   <td colname="col2"> Name of the audio track that failed to load, as specified in the manifest. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDIO_TRACK_LANGUAGE</span> </td> 
   <td colname="col2"> Language of the audio track, as specified in the manifest. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Seek errors</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_PERIOD</span> </td> 
   <td colname="col2"> ID of the period (integer). </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DESIRED_SEEK_POSITION</span> </td> 
   <td colname="col2"> <p>Position (in milliseconds) sought (double). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Miscellaneous</b> </td> 
   <td colname="col2"></td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AUDITUDE_ERROR_CODE</span> </td> 
   <td colname="col2"> Auditude error code (number). </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: DRM values {#section_D240082B93D34902A18C3923C1C717B3}

The Video Encoder interface of the Adobe video engine returns these DRM notifications in the `NATIVE_ERROR` metadata object.

When reporting DRM errors to Adobe, ensure that you include the `NATIVE_SUBERROR_CODE` and `DRM_ERROR_STRING` for troubleshooting assistance.

>[!TIP]
>
>This list provides TVSDK-specific information about the errors. For complete descriptions, see [ActionScript Run-Time Errors ActionScript Reference for the Adobe Flash Platform](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html#3300).

<table id="table_CD59A859865F4FFDBAA249C89C74770A"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Value for NATIVE_- ERROR_CODE metadata key </th> 
   <th colname="col2" class="entry"> Value for NATIVE_ERROR_NAME metadata key </th> 
   <th colname="col3" class="entry"> Meaning </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 3300 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidVoucher</span> </td> 
   <td colname="col3"> 
    <ul id="ul_516E4CB32D624B22892DDB9266CB04CA"> 
     <li id="li_348FC0F38B11417994119B61C9244076">What the distributor's software should do: 
      <ul id="ul_7AFD45CF92454BA4927783FAA628FBC4"> 
       <li id="li_0D9CCE61612643648C12DCDDD252E52A">If you are using Google Chrome, and you are in Incognito mode, and your Flash Player version is less than 11.6, this error might occur. <p>We recommend that the player check the browser's version number and advise the user to exit Incognito mode. </p> </li> 
       <li id="li_1DC6B755BD0840D48BEC92568FD330BA">Request the license again. <p>If the request is successful, you do not need to log or escalate. If the request is unsuccessful, log the content that caused the error. <span class="codeph"> subErrorId</span> contains a line error if present. </p> </li> 
      </ul> </li> 
     <li id="li_060B5D60C9BB419CBFA7B062FBCF2632">What the distributor should do: 
      <ul id="ul_FADB29DBF0DA4A0E8E54134AEB7DCD8A"> 
       <li id="li_FC5B1C04D21E4AECB0EBD9ADD3198504">If retries are unsuccessful on configurations other than Chrome with Flash less than version 11.6, a failure might have occurred in the packaging. </li> 
       <li id="li_A720ECE591254021879B335B81B1F76D">Check whether the issue is specific to certain content and repackage. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3301 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthenticationFailed</span> </td> 
   <td colname="col3"> <p>The server failed to authenticate or authorize the client. </p> 
    <ul id="ul_BE77AC1848FB4C09B6318359ACF1B8EE"> 
     <li id="li_6FB37D317D174E8488C5070D20CD241C">The distributor's software should take any action necessary to re-establish user's credentials or guide the user to acquire access to the content. </li> 
     <li id="li_BE071D59805B42D38E3E7650BC936417">The distributor should confirm that distributor's authorization and authentication mechanism is working correctly. <p>If the distributors are not planning to use the authentication or authorization features, they should check whether the policy of the offending content requires authentication and see Diagnosing policy / license discrepancies. </p> </li> 
    </ul> <p>For more information about this error code, see <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM error 3301 causes and resolution</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3302 </td> 
   <td colname="col2"><span class="codeph"> AAXS_RequireSSL</span> </td> 
   <td colname="col3"> <p>On Access 4.0 and above, this error is thrown on iOS when the remote key URL does not use HTTPS as the scheme. HTTPS is required. </p> 
    <ul id="ul_3D47777BBCA14B67B107FBBE3E37E40C"> 
     <li id="li_7F7BBB27AE754CC39ABAAF9269739C49">If distributor is using a version older than Access v4, or the version at least 4 but the platform is not iOS, the distributor's software should log the error. <p>The error is thrown only on iOS. </p> </li> 
     <li id="li_D83C427D2A0D47408F723EF7195070B6">If the distributor's software is at least Adobe Access version 4, and the platform is iOS, distributors must change the remote key server URL that they are using to HTTPS. <p>If they were only using HTTP, distributors might have to set up an HTTPS server. Otherwise, the distributors need to submit the logged information to Adobe and escalate the issue. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3303 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentExpired</span> </td> 
   <td colname="col3"> <p>The content you are viewing has expired according to the rules set by the content provider. subErrorId contains a client-specific error or line error. </p> <p> 
     <ul id="ul_1E4B3B8AE87A4E79997553BB2A0E52B9"> 
      <li id="li_EE3F2EEBF73743B9A38E4FCB7531E275">The distributor's software should attempt to reacquire license from the server once to determine whether a new non-expired license is available. <p>If no license is available or the license has expired, allow the user to acquire new license, or inform user that the content cannot be watched.If the content has been packaged with a policy that has a lapsed expiration/end date, the license server logs report a <span class="codeph"> PolicyEvaluationException</span> and state that the Policy End Date has lapsed (Server Error code 303). Check the server's log files to verify. </p> <p>If possible, customers should check the policy that they used during packaging to see whether it has expired. The Java command line tool is: 
        <code>
         java&nbsp;-jar&nbsp;libs/AdobePolicyManager.jar&nbsp;&nbsp;&nbsp;detail&nbsp;demo.pol
        </code> </p> </li> 
      <li id="li_50DBE680D8F04E7DA3E29C65A93188E7">The distributor should confirm whether license expiration dates are configured as intended. </li> 
     </ul> </p> <p>For more information about this error code, see <a href="https://forums.adobe.com/thread/1300813" format="https" scope="external"> 3303 (Content Expired) with AMS/FMS using a Live Stream?</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3304 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AuthorizationFailed</span> </td> 
   <td colname="col3">For more information about this error code, see <a href="https://forums.adobe.com/thread/1277149" format="https" scope="external"> DRM error 3301 causes and resolution</a>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3305 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerConnectionFailed</span> </td> 
   <td colname="col3"> <p>The connection to the license or domain servers timed out, either due to network delay or the client being offline. Normally subErrorId contains HTTP return code. </p> 
    <ul id="ul_938C7D8F07F64B4FA71A09DDF37E2E64"> 
     <li id="li_6648EA0049094E369BD9AE9CCA6B148D">The distributor's software should attempt a network connection to a known good server. <p>If the attempt fails, prompt the user to reconnect to the network. If the attempt is successful, log it. </p> </li> 
     <li id="li_2ECA2C04BA08449DA3AD79A52EFAA229">The distributor should verify that any license and domain servers in use are online and visible from the client's network. </li> 
    </ul> <p>For more information about this error code, see <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed] causes and resolution</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3306 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClientUpdateRequire</span> </td> 
   <td colname="col3"> Use a newer version of TVSDK for Android. <p>The current client cannot complete the requested action, but an updated client might be able to complete the request. </p> <p>This can have several causes: 
     <ul id="ul_2EC4D42D5273439FA1AFDA1A2578B3D6"> 
      <li id="li_FCA926F5FAED4E7190BE855545AB6ACF">A shared domain was used that is not available on this client. This is likely the case when playback works on Chrome, but not any other browser and vice versa. <p> <p>Tip: Chrome uses a different PHDS/PHLS key than the other browsers use. For more information, see <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </p> </li> 
      <li id="li_3B633FB699234DCEA136E9BE3CC3386D">The application is trying to add multiple DRMSessions when running on an iOS version that is earlier than 5.0. </li> 
      <li id="li_F7ED993AF0B941A7A27216B4D587A999">The metadata has a version of 3 or higher when only version 2 is supported. </li> 
     </ul> </p> 
    <ul id="ul_EE4AE6AD4F1745A5B5623E53B599DB62"> 
     <li id="li_7A83869D4262443DA35FA1DF8D3097DD">The distributor's software should alert the user and abort the operation. <p>If the software has a way of determining whether an upgrade is available, direct the user to that upgrade in the appropriate manner for the platform. </p> </li> 
     <li id="li_AF9C2711FDE54DA196EB9D2864632000">If the issue occurs because of a shared domain, the distributor will need to check with Adobe for an updated runtime or library. <p>For Flash runtime, the distributor can force the upgrade in their application directly. In the case of a library, the distributor will need to obtain an updated library, rebuild their application and deploy it to their users. </p> <p>If the issue occurs because of multiple DRMSessions, the distributor will need to update their application to check the iOS version number prior to adding multiple DRMSessions. Or they can restrict distribution of their application to iOS v5 and above. </p> <p>if the issue occurs because the metadata version is higher than version 2, the issue is probably corrupted metadata. They can try rebuilding the metadata and looking at the results. If they continue to see the problem, log the issue and escalate to Adobe. </p> </li> 
    </ul> <p>For more information about this error code, see <a href="https://forums.adobe.com/thread/1266675" format="https" scope="external"> How to remedy a 3306 DRMErrorEvent Error Code</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3307 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InternalFailure</span> </td> 
   <td colname="col3"> <p>This generally represents a bug in Adobe Access code and is unexpected, unless there's a known bug, as below. subErrorId contains a client-specific error or line error. </p> 
    <ul id="ul_79F4A9655A2148519B1E9509C41F78C3"> 
     <li id="li_0E093AB4D6BD489B852279E6C1525A15">If the browser is Chrome on Windows and Flash version is 11.6 (SWF version 19 or greater), the distributor's software should assume that the user pressed <span class="uicontrol"> Deny</span> on the infobar and treat the same as a 3368. </li> 
     <li id="li_0215D1089B344861A2C0A73E1067CFEF">If 3307 occurs when browser is not Chrome or Flash version is not 11.6, the distributor should escalate to Adobe. </li> 
    </ul> <p>Important: <span class="codeph"> 3307:1107296344 (FailedToGetBrokerHandle)</span> might happen with Chrome browser versions 24-28. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3308 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WrongLicenseKey</span> </td> 
   <td colname="col3"> <p>This error is throw whenever the license being used contains the wrong key to decrypt the content. subErrorId contains a client-specific error or line error. </p> <p>There seem to only be two ways of generating this bug: 
     <ul id="ul_1C955BD74C7843809D1B5A0CDCA5ED7B"> 
      <li id="li_18F0A7FDA6584887AD9DB3EDE54080D8">The customer has modified the standard Adobe tooling for generating licenses (for example, the licenser server Java framework). <p>In this case, the license contains a bad key which might not correspond to any content. </p> </li> 
      <li id="li_21D04ED1F1FA464785BC297D385766FF">The customer has issued multiple licenses with the same license ID. <p>In this case, there are multiple licenses that are available on the client that match the content metadata and the Access code has selected the wrong one for use. </p> </li> 
     </ul> </p> 
    <ul id="ul_64AEE62BE36946F290067CF475A36ECA"> 
     <li id="li_9EEB2B11A4DA41E78C5840D8FAA81F0D">The distributor's software should attempt to reacquire license from the server. 
      <ul id="ul_ACADC5518B054D0A853AEED2B675DB23"> 
       <li id="li_394835C8731048A5BF7D9370AC12448C">If no license is available or license is expired, provide workflow for user to acquire new license, or inform user that the content cannot be watched and log the issue. </li> 
       <li id="li_3FE50518BE53405F9563FA620F7EAD5F">If this was a domain bound content (for AIR), provide a way for the user to join the domain. </li> 
      </ul> </li> 
     <li id="li_C80B353C1AEA4E9398241420CB491E84">The distributor should: 
      <ul id="ul_B5C50009374C4EED9B2B050B48F5F0F6"> 
       <li id="li_D5E6B760E0BC4B5C949ED1544B398838">Verify that they have not customized the license issuance portions of the Access License server. </li> 
       <li id="li_AA8F4E4B6DDD40BA8807C0920A92186B">Verify that they are issuing unique license IDs for all licenses. </li> 
       <li id="li_A2C53FE779AC4FDDB65E00A2C4F43EC4">Escalate the issue with Adobe. </li> 
      </ul> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3309 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedAdditionalHeader </span> </td> 
   <td colname="col3"> <p>This will occur if the header is larger than 65536 bytes. </p> 
    <ul id="ul_82C0F688519B4F43A764D59A891F1903"> 
     <li id="li_E66AC9149A0649E88A79C5289C12C395">The distributor's software should Log which piece of content caused the error. </li> 
     <li id="li_1C5916A33E7B4DC9968105B9BD20A727">The distributor should confirm that error is reproducible with specific pieces of content. Repackage broken content. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3310 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppIDMismatch </span> </td> 
   <td colname="col3">The Android application does not match the one in use. <p>The correct AIR application or Flash SWF is not being used. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3311 </td> 
   <td colname="col2"><span class="codeph"> AAXS_AppVersionMismatch </span> </td> 
   <td colname="col3"> Not in use. This issue might still be generated by the version 1.x stack in AIR. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3312 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LicenseIntegrity </span> </td> 
   <td colname="col3"> To fix this, redownload the license from the server. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3313 </td> 
   <td colname="col2"><span class="codeph"> AAXS_WriteMicrosafeFailed </span> </td> 
   <td colname="col3"> <p>This issue occurs when the system cannot write to the file system. <span class="codeph"> subErrorId</span> contains a client-specific error or line error. </p> <p>On Microsoft Windows, error 3313 might be thrown by Active X or NPAPI plug flash player when the encrypted content has a licenseID or a policyID that is too long. This is because of the maximum path length in Windows. (Pepper plugin does not have this problem.) </p> <p>See watson 3549660 </p> 
    <ul id="ul_DFD527D1E1224A439766DF7BED878E3B"> 
     <li id="li_FAF8FD98A4E8478CA7A92F770676ADFC">The distributor's software should prompt the user to confirm that their user directory is not locked nor on a volume that is full or locked. </li> 
     <li id="li_6D1136EA750A459BBECEEE5F73F527BB">If the distributor is using AIR, rather than Flash, the issue might be caused by a path length limitation. <p>Distributors should shorten the name of their AIR applicaiton to something reasonable. Also, publish contents again with a shorter <span class="codeph"> licenseID</span> and a <span class="codeph"> policyID</span>. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3314 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptedDRMMetadata </span> </td> 
   <td colname="col3"> <p>This error often indicates that the content was packaged with test PKI certs, and the player is built with production PKI or vice versa. subErrorId contains a client-specific error or line error. </p> 
    <ul id="ul_A122EF304CAF48A8B4DA1E3F4413E29B"> 
     <li id="li_A9A1A5B23E884C22A71E2DE7535FEB3B">The distributor's software should log which piece of content caused the error. </li> 
     <li id="li_7AD7F13A4B1B4998A7E49664E7645815">The distributor should confirm that the error is reproducible with specific pieces of content. <p>You might have to repackage broken content. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3315 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PermissionDenied </span> </td> 
   <td colname="col3"> <p>There are known bugs in which this error code is thrown when a 3305 is intended. For more information, see <a href="https://forums.adobe.com/thread/1284947" format="https" scope="external"> DRM 3305 [ServerConnectionFailed] causes and resolution</a>. </p> <p>Remote SWF loaded by AIR is not allowed to access Flash Access functionality. This error code can also be thrown if a security error occurs during network access. Examples include the destination server does not the client to connect by using crossdomain.xml, or the crossdomain.xml is not reachable. </p> <p>For more information, see <a href="https://forums.adobe.com/thread/1266592" format="https" scope="external"> DRM error 3315 possible root cause and resolution</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3316 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NOTUSED_MOVED </span> </td> 
   <td colname="col3"> Was <span class="codeph"> ADOBECPSHIM_MinorErr_MissingAdobeCPModule</span>. Moved to 3344 due to conflict with Flash error code. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3317 </td> 
   <td colname="col2"><span class="codeph"> AAXS_LoadAdobeCPFailed </span> </td> 
   <td colname="col3"> <p>Important:  This is a rare error and usually does not occur in a production environment. </p> <p>If the error does occur, you can do one of the following: 
     <ul id="ul_BC435E61623444BB98A86216531DC892"> 
      <li id="li_FA433D0758B642D2AFDCF04906B3FE18">If you are using AIR, reinstall it. </li> 
      <li id="li_F08D9AAFF46244F8842DEE5FD9CBBE0A">If you are using Flash Player, download the <span class="codeph"> AdobeCP</span> modules again. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3318 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncompatibleAdobeCPVersion </span> </td> 
   <td colname="col3"> Not applicable for Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3319 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPGetAPI </span> </td> 
   <td colname="col3"> Not applicable for Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3320 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HostAuthenticateFailed </span> </td> 
   <td colname="col3"> Not applicable for Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3321 </td> 
   <td colname="col2"><span class="codeph"> AAXS_I15nFailed </span> </td> 
   <td colname="col3"> <p>The process of provisioning the client with keys failed. subErrorId contains a client-specific, server-specific or line error. </p> 
    <ul id="ul_98D919B9060A441AACB6106F6D8E8DA7"> 
     <li id="li_DCAB00A8AC4A426CBBD377374B3F71AE">The distributor's software should retry the operation at least once. <p>If you are using Google Chrome on Windows, provide an explanation about how to allow plugin access that is not in a sandbox. Google Chrome's unsandbox access denied</a>. </p> </li> 
     <li id="li_7FB7681FE32D444BB1BDBA3E5953A2C3">The distributor should complete one of the following tasks: 
      <ul id="ul_486B64F187C44AE3B4775953A6142836"> 
       <li id="li_095B1D4CD051427CB2BFA7082B454056">If the error is consistent across platforms, you should escalate the issue with Adobe. </li> 
       <li id="li_0C6EB7B912FA41E59657216498DA3515">If the error is confined to Chrome on Windows, guide the user to allow unsandboxed plugin access. </li> 
      </ul> <p>Distributors should update their SWF to version 19 or later, and the Chrome-specific 3321 error, a 3368 error is thrown. Error 3368 can be handled more specifically by the distributor's software. This change was introduced in Chrome Stable channel version 26.0.1410.43. </p> <p>Tip: Error <span class="codeph"> 3321:1090519056</span> might happen with Flash Player versions 11.1 to 11.6. We recommend that you upgrade to the latest Flash Player version. </p> </li> 
    </ul> <p>For more information, see <a href="https://forums.adobe.com/thread/1277138" format="https" scope="external"> DRM error 3321 Causes &amp; Resolution</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Global Store corruption errors</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3322 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DeviceBindingFailed </span> </td> 
   <td colname="col3"> <p>The device does not appear to match the configuration that was present when initialized. subErrorId contains a client-specific or line error. </p> <p>The distributor's software should complete one of the following tasks: 
     <ul id="ul_444401051A2E407B95BC44491E9BB71C"> 
      <li id="li_93493EA05DB44CB1AEC368663F1ABA8D"> <p>If the device is not using Flash Player, and is using AIR, iOS, and so on, call <span class="codeph"> DRMManager.resetDRMVouchers()</span>. </p> <p>If the issue occurs on iOS in a development phase, ask the developer to confirm whether the issue is observed when switching between builds that were downloaded from third-party, pre-release distribution systems (for example, HockeyApp) and a local build from Xcode. Attributes of a previous installation are not entirely overwritten when switching between a build distributed from HockeyApp and a build from Xcode. This situation might trigger the 3322 error. </p> <p>To resolve this issue, the developer should remove the older build from the device before installing the new build. </p> </li> 
      <li id="li_A5C9633F11584C788A2D9A23CC18FA6D">If the device is using Flash Player, and it is unusable from a 3322 or 3346 error codes, see the instructions from Adobe about how to programmatically reset your DRM license store on <a href="https://forums.adobe.com/message/5535907#5535907" format="https" scope="external"> DRM Error 3322/3346/3368 in Chrome (Info-Bar Problems)</a>. </li> 
     </ul> </p> <p>This error is not expected to occur frequently. In corporate environments that uses roaming profiles, if a user was viewing content that is protected by DRM, the chances error 3322 occurring increases as the user logs in from different machines. If possible, distributor should try to get this information from user. </p> <p>If the error occurs frequently, escalate to Adobe. You must notify Adobe whether resetting license store did (or did not) solve the problem and tell Adobe on which browsers the error is occurring. </p> <p>For more information, see the following articles: 
     <ul id="ul_C468409D1EA046178CA7F54DCDCB84EA"> 
      <li id="li_20C8CA3853574CE486F21E7A3667DAB9"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> https://forums.adobe.com/message/5520902</a> </li> 
      <li id="li_6E6F1BD6FE7843449B3E2F06F342EFF7"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> https://forums.adobe.com/message/5535911</a> </li> 
      <li id="li_2BE40E513A0C4BAD900C7B69FEF5D690"><a href="https://forums.adobe.com/message/5748618" format="https" scope="external"> https://forums.adobe.com/message/5748618</a> </li> 
      <li id="li_9C2BD122E3874E2893DD43E082A877E0"><a href="https://forums.adobe.com/message/6061165" format="https" scope="external"> https://forums.adobe.com/message/6061165</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3323 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptGlobalStateStore </span> </td> 
   <td colname="col3"> <p>Files used by the DRM client have been modified unexpectedly. subErrorId contains a client-specific or line error. </p> 
    <ul id="ul_96EA771046CA4B2B9FAE24D493F43FF2"> 
     <li id="li_D2693CD8EFEF46108828BA17E3F54FF6">The distributor's software should guide the user to reset in the same way as for 3322. </li> 
     <li id="li_0149B82436B64E28AC2B8C9B0EB09898">If the GlobalStore is failing at a rate greater than the expected failure rate of the hard drives of your user base, escalate the issue to Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3324 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MachineTokenInvalid </span> </td> 
   <td colname="col3"> Reset DRM local storage for this application. Call DRMManager.resetDRM. <p>The license server might not be able to connect to the Certificate Revocation List (CRL) server to refresh its CRL files, or the client machine is requesting a license/authentication that has been revoked by the license server. </p> <p>In the server logs, an error code 111 is MachineTokenInvalid. However, at the client level, error code 111 is translated to error code 3324. </p> <p>The DRM license server administrator should check whether the customer's license server has ever been able to retrieve the Adobe CRL files. If the customer is using Tomcat, the customer can check the<span class="filepath"> tomcat/temp/</span> directory to see whether there are 4 CRL files. </p> 
    <ul id="ul_23B7F1A104AF49E79EA87DB8E15E337E"> 
     <li id="li_855D87F251184FE688A8D5FA0F6C9EF5">If the files are in this directory, double-click the files in Windows Explorer and in the CRL viewer application, determine whether any of the files have expired. </li> 
     <li id="li_58EC4EDA2B5146188A0FF7B33C91E2FD">If there are no files in tomcat/temp/, then it can be assumed this license server has never been able to reach the Adobe CRL server due to a firewall/routing issue. </li> 
    </ul> <p>For more information, see <a href=https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_secure_deployment_guidelines.pdf format="http" scope="external"> Firewall rules</a>. </p> <p>If the CRL files are not available or have expired, you must confirm whether the license server can be reached. Open a network sniffer on the customer's license server, restart the server, and have a client attempt to request a license from the server. You can observe the network traffic to see whether calls to the following URL endpoints are successful: <p>Tip:  You can also enter the following CRL URLs in a browser to see whether you can manually download each file. </p> 
     <ul id="ul_9B65C7ABBDEC4AC9BF3755FFD3587971"> 
      <li id="li_6867A9050E8D421C9138AC853D1784C9"><a href="https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl</a> </li> 
      <li id="li_6431689260554EAFAFDA2EC31798DCB5"><a href="https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl</a> </li> 
      <li id="li_2939674D0F854ADEB67E45FD216288A2"><a href="https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl" format="http" scope="external"> crl2.adobe.com/Adobe/FlashAccessRootCA.crl</a> </li> 
      <li id="li_96386E00BE9D4CB99D100057A5F7C6DD">crl3.adobe.com/AdobeSystemsIncorporated FlashAccessRuntime/LatestCRL.crl</li> 
     </ul> </p> <p>If the firewall rules are open and there are no current 3324 errors, there might have been a temporary network issue. Check the customer's server logs, which are probably in the <span class="codeph"> /tomcat/logs/</span> directory, to determine whether an error occurred when the license server tried to fetch the Certificate Revocation Lists. <p>Important:  An error might occur when a large number (or a burst) of clients report a 3324 error to a temporary network issue when renewing a CRL file. When the network issue was resolved, the 3324 issues were also resolved. </p> </p> <p>If all 4 of the CRL files exist in the <span class="filepath"> tomcat/temp/</span> directory, and clients are still getting 3324 error codes, there might be file access issues to the CRL files. To resolve this issue, you might want to review the logs and purge the existing CRL files. </p> <p>If there are no server issues, prompt the user to reset in as described in 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Server Store corruption errors</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3325 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CorruptServerStateStore </span> </td> 
   <td colname="col3"> <p>Files used by the DRM client have been modified unexpectedly. <span class="codeph"> subErrorId</span> contains a client-specific or line error. </p> 
    <ul id="ul_860D2402DA61460AB0D938F1116F6D64"> 
     <li id="li_CF368C43452B4265B62ADA3E223894BA">The distributor's software should retry the operation again, because AdobeCP has deleted the offending server store internally, and a retry should succeed. If retry fails, log the issue. </li> 
     <li id="li_51A5803A1F754970BB4EBD6494F5DC96">If retries are failing at a rate greater than the expected failure rate of the hard drives of your user base, escalate the issue to Adobe. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3326 </td> 
   <td colname="col2"><span class="codeph"> AAXS_StoreTamperingDetected </span> </td> 
   <td colname="col3"> Call <span class="codeph"> DRMManager.resetDRM</span>. <p>The License store has been tampered/corrupted and can no longer be used. </p> <p>The distributor's software should guide the user to reset in the same way as described in 3322. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3327 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ClockTamperingDetected </span> </td> 
   <td colname="col3"> Fix the clock or acquire <span class="codeph"> Authn/Lic/Domain</span> license again. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><b>Authentication/License/Domain server errors</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3328 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerErrorTryAgain </span> </td> 
   <td colname="col3"> <p>This is a server-side error where the server was unable to complete the request from the client. This error can occur when, for example, the server is busy, HTTP/500, the server does not have the needed key to decrypt the request, and so on. </p> <p>On the client, there is no way to determine what went wrong. The customer must review the Adobe Access server logs, which are usually called <span class="codeph"> AdobeFlashAccess.log</span>, to determine what went wrong. There is always a descriptive stack trace in the log to indicate the problem. <span class="codeph"> subErrorId</span> contains a server-specific or line error. </p> <p>The distributor should look at server logs to identify which server is sending this error. For 3328 errors that has a sub-error code 101, the server cannot decrypt the request. The customer must validate that the license / transport server certificates that are installed on the license server match and correspond with the certificates that is used during packaging. </p> <p>In addition, if customers are using the Reference Implementation, they must ensure that there are no typos in the <span class="codeph"> flashaccess-refimpl.properties</span> file where the primary and additional certificates are specified. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3329 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ApplicationSpecificError </span> </td> 
   <td colname="col3"> <p>The application-specific sub error code is not known to Flash Access. <span class="codeph"> subErrorId</span> contains a server-specific error from the publishers customized license server. The server returned an error in the application-specific namespace. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3330 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NeedAuthentication </span> </td> 
   <td colname="col3"> <p>This error occurs when the content is configured to ask clients to authenticate before getting the licenses. </p> 
    <ul id="ul_712D29B8B5A6401FB014C4A283918E32"> 
     <li id="li_2D56905EB50D4FDEAD69CA8EAE38AD1A">The distributor's software should authenticate the user and then acquire the license again. <p>If your service does not intend to use authentication, log the identify of the content that is causing this error. </p> </li> 
     <li id="li_B3BCF899B8BE41C7A4F7CF84B0503483">This error should not require an escalation, unless the content is not supposed to be configured to require authentication. <p>In this case, repackage the offending content with proper policy. If the content is packaged correctly, see Diagnosing policy / license discrepancies. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>License Enforcement errors that aren't covered above</b> </td> 
   <td colname="col2"> </td>
   <td colname="col3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"> 3331 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentNotYetValid </span> </td> 
   <td colname="col3"> <p>The acquired license is not yet valid. To resolve this issue, check whether the client clock is not set correctly. To set the client clock, repackage the content or modify the license server configuration. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3332 </td> 
   <td colname="col2"><span class="codeph"> AAXS_CachedLicenseExpired </span> </td> 
   <td colname="col3"> Reacquire license from the server. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3333 </td> 
   <td colname="col2"><span class="codeph"> AAXS_PlaybackWindowExpired </span> </td> 
   <td colname="col3"> <p>You must notify users that they cannot play this content till the policy expires. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3334 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMPlatform </span> </td> 
   <td colname="col3"> <p>This platform is not allowed to playback the content because, for example, the content provider has configured Adobe Access to deny content to Adobe Access on a platform or a shared domain-bound license is bound to a shared domain token that is meant for a different partition. </p> <p>CDM might throw this error if content was not packaged by using an appropriate (CDM feature gated) packager certification. </p> <p>If the content is packaged with an incorrect PHDS/PHLS certificate, the content might work in Chrome but not other browsers (or vice versa). <p>Tip:  This is because Chrome uses different PHDS/PHLS certificates. </p>To confirm which certificate is being used, dump the details of the content metadata and look for the <i>recipient certificates</i>. For more information, see <a href="https://adobeprimetime.zendesk.com/agent/tickets/2891" format="https" scope="external"> https://adobeprimetime.zendesk.com/agent/tickets/2891</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3335 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidDRMVersion </span> </td> 
   <td colname="col3"> Upgrade to the latest version of the TVSDK for Android. <p>To resolve this issue, complete one of the following tasks: 
     <ul id="ul_BF1742948BC9461CB8686DE70124D3CD"> 
      <li id="li_690D440C94CC45A0AE55EC319B1C4C23">Upgrade AIR </li> 
      <li id="li_CDD20251C881466E88BE7BBB53D61EBC">For Flash Player, upgrade the AdobeCP module and retry playback. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3336 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimePlatform </span> </td> 
   <td colname="col3"> <p>This platform is not allowed to playback the content because, for example, the content provider has configured Access to deny content to FP/AIR on a platform. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3337 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InvalidRuntimeVersion </span> </td> 
   <td colname="col3"> Upgrade to the latest version of TVSDK for Android. <p>This occurs if the content or the server is configured to deny playback to a particular version of the Flash or AIR runtimes. </p> 
    <ul id="ul_B0732D941256483CABBDD30C9BF43249"> 
     <li id="li_72782B1D638F48C0B87084689FB9C798">If the user is on an operating system on which Flash can be upgraded, the distributor's software should prompt the user to upgrade Flash and try again. Otherwise advise the user to use a different machine. </li> 
     <li id="li_1E3FD93CE39E43F2B7D961299B1211DA">If error 3337s is suspected, identify whether it is occurring for specific content and repackage that content. If content is packaged correctly see Diagnosing policy / license discrepancies </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3338 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnknownConnectionType </span> </td> 
   <td colname="col3"> <p>Unable to detect the connection type, and the policy requires you to turn on Output Protection. This issue is expected only if the content is packaged to require digital or analog output protection. </p> <p>An issue in versions of Flash Player older than version 11.8.800.168 caused error 3338 to occasionally occur on content for which the policy indicated that content protection is <span class="codeph"> USE IF AVAILABLE</span>. This issue is fixed in version 11.8.800.168 and later. </p> 
    <ul id="ul_4B6CA26A53F84838B5B95400925464D4"> 
     <li id="li_CBD890F467E449EBB5116E1561252058">The distributor's software select a variant of the content that does not require output protection (for example SD variant of an HD stream). <p>If error 3338 is occurring on <span class="codeph"> USE_IF_AVAILABLE </span> content, check for player version number. If the player version is less than 11.8.800.168, advise the user to upgrade Flash Player. If error 3338 is occurring on versions above 11.8.800.168, log which content caused the error. </p> </li> 
     <li id="li_62886C1D96264B129928A7E29E6C70E1">The distributor should check which content is causing this error and validate that the content's policy is setting <span class="codeph"> NO_PROTECTION</span> or <span class="codeph"> USE_IF_AVAILABLE</span> for analog and digital outputs. <p>If content is inadvertently packaged with <span class="codeph"> NO_OUTPUT</span> or <span class="codeph"> REQUIRED</span>, repackage the content. If content is packaged correctly see Diagnosing policy / license discrepancies. Otherwise escalate to Adobe. </p> </li> 
    </ul> <p>For more information, see <a href="https://forums.adobe.com/message/5518688" format="https" scope="external"> Getting unexpected 3338 errors when your DRM policy is set to USE_IF_AVAILABLE?</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3339 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogPlaybackAllowed </span> </td> 
   <td colname="col3"> Unable to play back on analog device. To resolve the issue, connect a digital device. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3340 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoAnalogProtectionAvail </span> </td> 
   <td colname="col3"> Unable to play back content because the connected analog external display device (monitor/TV) does not have the correct capabilities (for example, the device does not have Macrovision or ACP). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3341 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalPlaybackAllowed </span> </td> 
   <td colname="col3"> Unable to play back content on a digital device. <p>Important:  This issue should not happen in a production environment, because content publishers should not disallow digital playback. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3342 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDigitalProtectionAvail </span> </td> 
   <td colname="col3"> The connected digital external display device (monitor/TV) does not have the correct capabilities. For example, the device does not have HDCP. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3343 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IntegrityVerificationFailed </span> </td> 
   <td colname="col3"> <p>Not applicable for Android. </p> <p>This error is currently known to happen initially after a new version of Flash is released. It occurs because Flash upgraded while Flash was open, which puts Flash in a bad state until browser restarts. </p> 
    <ul id="ul_A0AC4A77550E40409A04BD33748EA987"> 
     <li id="li_F41C1ABD838D41ABB0DF65093E664A29">The distributor's software should complete the following tasks: 
      <ul id="ul_79B2AB1372074D448F129851AA24F985"> 
       <li id="li_B93EDD263D78434FAF198A01938D3508">Recommend that the user close or quit all browsers and then reopen. </li> 
       <li id="li_ADFBCFA66AD849E18DB390455458528E">Check if the version of Flash is current. <p>If the version is not current, advise the customer to upgrade, close all tabs in their browser, and reopen. </p> </li> 
      </ul> </li> 
     <li id="li_281B54582B5949AEA7D166246917EE41">If error appears to occur after a successful browser restart, escalate to Adobe. <p>When a new version is released, we recommend that you contact Adobe Support to see whether the background updates issue has been fixed. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3344 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MissingAdobeCPModule </span> </td> 
   <td colname="col3"> Not applicable for Android. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3345 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DRMNoAccessError </span> </td> 
   <td colname="col3"> <p>Not applicable for Android. </p> <p>This error occurs when part of Flash or AIR was not installed correctly. </p> <p>The distributor's software should do one of the following: 
     <ul id="ul_D1188E2D4FDF4BD89A04F5629D75D981"> 
      <li id="li_B33FBCA5D4534D668B86A5E93DB3A809">Ask the user to uninstall and reinstall AIR. </li> 
      <li id="li_B7D2388E9FA84C26AF1C87B48AF9EF16">For Flash Player, call <span class="codeph"> System.update</span>. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3346 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MigrationFailed </span> </td> 
   <td colname="col3"> 
    <ul id="ul_518AD4931CC64EB3A962DD451E6C5067"> 
     <li id="li_3C44F0740B08490E9C62D89C40B57DC2">The distributor's software should do one of the following: 
      <ul id="ul_7D90526684BF4EB2BBADCF598AA13086"> 
       <li id="li_D15B4BEDAF7340F6B9BC886DF6E346EC">If AIR, call <span class="codeph"> DRMManager.resetDRMVouchers()</span> </li> 
       <li id="li_40A51D35408249CFA28DBC49FDA3408B">If Flash has is unusable because of errors 3322 or 3346 error code, users should go to <a href="https://forums.adobe.com/message/5535907#5535907" format="http" scope="external"> https://forums.adobe.com/message/5535907#5535907</a> and follow the Adobe article's instructions to programmatically reset their DRM license store. </li> 
      </ul> </li> 
     <li id="li_0464471E4A094C80BF2986694341921A">If this error occurs frequently, the distributor should provide the details about the frequency player version and the browser version to Adobe. </li> 
    </ul> <p>For more information, see the following forum articles: 
     <ul id="ul_44E0077FEAA749CC9549BF3846065304"> 
      <li id="li_2BE3B2443380415DA73B7AA3B6547B31"><a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> DRM Error 3322/3346/3368 in Chrome (Info-Bar Problems)</a> </li> 
      <li id="li_4E5C7414756644E1AB78BE7B8112228C"><a href="https://forums.adobe.com/message/5535911" format="https" scope="external"> 3322 or 3346 error after hardware change</a> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3347 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InsufficientDeviceCapabilites </span> </td> 
   <td colname="col3"> <p>The primary meaning of this error is that the license has a constraint which the clients' DRM certificate indicates it cannot satisfy. The following "hardware capabilities" are defined when the clients DRM certificate is issued: 
     <ul id="ul_1EB6F1469C244CF0BA52C212495C053D"> 
      <li id="li_646043CE045C4DE2BBC939E1F4963DFE"><b>Non-User Accessible Bus</b>. If <b>true</b>, the decrypted media never flows across a bus or into main memory where an application can access to it. <p>If <b>false</b>, content might be accessible to the application after decryption. </p> </li> 
      <li id="li_02AAECAF4D35447BA10554541B46DE67"><b>Hardware Root of Trust</b>. If <b>true</b>, all software that is loaded at boot time on the device was validated against a key or digest that is only available in hardware. <p>Both of these constraints are checked on the client side when the license is opened against the DRM certificate for the client and failure is immediate. These constraints can also be checked on the server side prior to issuing the license. </p> </li> 
     </ul> </p> <p>The secondary meaning of this error is that the license has the "Jailbreak Enforcement" policy set and a jailbreak has been detected on the device. This check is done periodically on the client side and cannot be checked on the server side. </p> <p>The distributors can update the policies and remove the restrictions. For device capability policies, issue the policy update command with the <span class="codeph"> -devCapabilitiesV1</span> flag and no arguments. For jailbreak enforcement, set <span class="codeph"> policy.enforceJailbreak=false</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3348 </td> 
   <td colname="col2"><span class="codeph"> AAXS_HardStopIntervalExpired </span> </td> 
   <td colname="col3"> Hard stop interval expired. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3349 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooHigh </span> </td> 
   <td colname="col3"> The server is running at a version that is higher than the highest version that is supported by client. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3350 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ServerVersionTooLow </span> </td> 
   <td colname="col3"> The server is running at a version that is lower than the minimum version that is supported by client. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3351 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenInvalid </span> </td> 
   <td colname="col3"> Domain token was invalid. To resolve this issue, register with the domain again. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3352 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooOld </span> </td> 
   <td colname="col3"> The domain token is older than the token that is required by the license. To resolve the issue, register with the domain again. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3353 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenTooNew </span> </td> 
   <td colname="col3"> The domain token is newer than the token that is required by the license. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3354 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainTokenExpired </span> </td> 
   <td colname="col3"> Domain token has expired. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3355 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainJoinFailed </span> </td> 
   <td colname="col3"> Domain join failed. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3356 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCorrespondingRoot </span> </td> 
   <td colname="col3"> A root license for a V3 leaf license was not found. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3357 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoValidEmbeddedLicense </span> </td> 
   <td colname="col3"> No valid embedded license was found. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3358 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoACPProtectionAvail </span> </td> 
   <td colname="col3"> Cannot play back because the connected analog device does not have ACP protection. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3359 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoCGMSAProtectionAvail </span> </td> 
   <td colname="col3"> Cannot play back because connected analog device does not have CGMS-A protection. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3360 </td> 
   <td colname="col2"><span class="codeph"> AAXS_DomainRegistrationRequired </span> </td> 
   <td colname="col3"> Content requires domain registration. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3361 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NotRegisteredToDomain </span> </td> 
   <td colname="col3"> Machine is not registered to the domain for the specified metadata. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3362 </td> 
   <td colname="col2"><span class="codeph"> AAXS_OperationTimeoutError </span> </td> 
   <td colname="col3"> Asynchronous operation took longer than <span class="codeph"> maxOperationTimeout</span>. Only returned by iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3363 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UnsupportedIOSPlaylistError </span> </td> 
   <td colname="col3"> The M3U8 playlist passed in had unsupported content. Only returned by iOS DRMNative Framework. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3364 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoDeviceId </span> </td> 
   <td colname="col3"> <p>The framework requested the device ID, but the returned value was empty. </p> <p>The user should not select the <span class="uicontrol"> Allow identifiers for protected content</span> check box in Chrome settings. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3365 </td> 
   <td colname="col2"><span class="codeph"> AAXS_IncognitoModeNotAllowed </span> </td> 
   <td colname="col3"> <p>This browser/platform combination does not allow DRM-protected playback in Incognito mode. </p> <p>The distributor's software should advise the user to exit Incognito mode or use a different browser. For more information, see <a href="https://forums.adobe.com/thread/1266622" format="https" scope="external"> DRM error 3365 cause and resolution</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3366 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadParameter </span> </td> 
   <td colname="col3"> <p>The host runtime called the Access library with a bad parameter. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3367 </td> 
   <td colname="col2"><span class="codeph"> AAXS_BadSignature </span> </td> 
   <td colname="col3"> m3u8 manifest signing failed. Only returned by iOS DRMNative Framework or AVE. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3368 </td> 
   <td colname="col2"><span class="codeph"> AAXS_UserSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>The user cancelled the operation or has entered settings that disallow access to the system. </p> <p>This error is only thrown when the SWF version is 19 or later. For backward compatibility, 3321 is thrown when the SWF is version 18 or earlier. </p> <p>The distributor's software should guide the user to an explanation of how to allow unsandboxed plugin access. Google Chrome's unsandbox access denied</a> and <a href="https://forums.adobe.com/message/5520902" format="https" scope="external"> DRM Error 3322/3346/3368 in Chrome (Info-Bar Problems)</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3369 </td> 
   <td colname="col2"><span class="codeph"> AAXS_InterfaceNotAvailable</span> </td> 
   <td colname="col3"> <p>A required browser interface is not available. This issue occurs only on Pepper. There could be a mismatch between the Flash plugin and the browser version. </p> <p>The distributer's software should guide the user to ensure that they have the latest version of the browser installed. </p> <p> If the incidences of this error are increasing, and corresponds to a browser update being released, escalate to Adobe. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3370 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ContentIdSettingsNoAccess</span> </td> 
   <td colname="col3"> <p>The user has disabled the <span class="uicontrol"> Allow identifiers for protected content</span> setting. </p> <p>Tip:  This error appeared with Pepper versions 13.0.0.x or greater. </p> <p>The distributor's software should guide the user to enable the <span class="uicontrol"> Allow identifiers for protected content</span> setting. </p> <p>The distributor's operations team should guide the user to enable the <span class="uicontrol"> Allow identifiers for protected content</span> setting. </p> <p>For more information, see <a href="https://forums.adobe.com/message/6518323#6518323" format="https" scope="external"> https://forums.adobe.com/message/6518323#6518323</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3371 </td> 
   <td colname="col2"><span class="codeph"> AAXS_NoOPConstraintInPixel</span><span class="codeph"> Constraints</span> </td> 
   <td colname="col3"> <p>Malformed resolution based on output protection constraints in the license. </p> <p>The distributor's software should display an error message. Ask user to report the problem to the distributor with a content title. </p> <p>The distributor should repackage content with a valid policy. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3372 </td> 
   <td colname="col2"><span class="codeph"> AAXS_ResolutionLargerThanMaxResolution</span> </td> 
   <td colname="col3"> <p>The content's resolution is larger than the maximum resolution that is specified in the output-protection constraint. </p> <p>If the distributor's operations team sees this error in their logs, they should review the resolution-based output protection policy, and if necessary, repackage the content. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3373 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_DisplayResolutionLargerThanConstrain</span> </td> 
   <td colname="col3"> <p>The content's resolution is larger than the resolution that is specified by the currently active output-protection constraint. </p> <p>If the distributor's operations team sees this error in their logs, they should review the resolution-based output protection policy, and if necessary, repackage the content. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3374 </td> 
   <td colname="col2"><span class="codeph"> AAXS_MinorErr_ClientCommProcessFailed</span> </td> 
   <td colname="col3"> <p>Failed during client-side communication processing, for example, request generation, response processing, bad auth token, and so on. </p> <p>If the distributor's operations team sees this error in their logs, they should review the resolution-based output protection policy, and if necessary, repackage content. </p> </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Video playback values {#section_7079501250C2487499639F92EC774525}

The Video Encoder interface of the AVE returns these video playback notifications in the `NATIVE_ERROR` metadata object. 

<table id="table_5EEB1F60E5854452A8B0BABBE9B32651"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Value for NATIVE_ERROR_CODE metadata key </th> 
   <th colname="col2" class="entry"> Value for NATIVE_ERROR_NAME metadata key </th> 
   <th colname="col3" class="entry"> Description </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> -1 </td> 
   <td colname="col2"><span class="codeph"> END_OF_PERIOD</span> </td> 
   <td colname="col3"> End of period. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 0 </td> 
   <td colname="col2"><span class="codeph"> SUCCESS</span> </td> 
   <td colname="col3"> Operation successful. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 1 </td> 
   <td colname="col2"> <span class="codeph"> ASYNC_OPERATION_IN_PROGRESS</span> </td> 
   <td colname="col3"> Asynchronous operation. The operation request has been made. Success/failure information will be available later. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 2 </td> 
   <td colname="col2"><span class="codeph"> EOF</span> </td> 
   <td colname="col3"> Operation not possible due to end of file (EOF) condition. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 3 </td> 
   <td colname="col2"><span class="codeph"> DECODER_FAILED</span> </td> 
   <td colname="col3"> The decoder failed at runtime. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 4 </td> 
   <td colname="col2"><span class="codeph"> DEVICE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Failed to open hardware decoder. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 5 </td> 
   <td colname="col2"><span class="codeph"> FILE_NOT_FOUND </span> </td> 
   <td colname="col3"> Resource cannot be located. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 6 </td> 
   <td colname="col2"><span class="codeph"> GENERIC_ERROR </span> </td> 
   <td colname="col3"> Generic error. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 7 </td> 
   <td colname="col2"><span class="codeph"> IRRECOVERABLE_ERROR </span> </td> 
   <td colname="col3"> An error condition that the Video Engine cannot recover from. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 8 </td> 
   <td colname="col2"><span class="codeph"> LOST_CONNECTION_RECOVERABLE </span> </td> 
   <td colname="col3"> Network error, trying to recover. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 9 </td> 
   <td colname="col2"><span class="codeph"> NO_FIXED_SIZE </span> </td> 
   <td colname="col3"> The size of the resource cannot be determined. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 10 </td> 
   <td colname="col2"><span class="codeph"> NOT_IMPLEMENTED </span> </td> 
   <td colname="col3"> Feature not implemented. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 11 </td> 
   <td colname="col2"><span class="codeph"> OUT_OF_MEMORY </span> </td> 
   <td colname="col3"> Out of memory. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 12 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR </span> </td> 
   <td colname="col3"> Error while parsing the media file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 13 </td> 
   <td colname="col2"><span class="codeph"> SIZE_UNKNOWN </span> </td> 
   <td colname="col3"> The resource has a size, but it is unknown. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 14 </td> 
   <td colname="col2"><span class="codeph"> UNDER_FLOW </span> </td> 
   <td colname="col3"> Underflow condition. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 15 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_CONFIG </span> </td> 
   <td colname="col3"> Configuration is not supported. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 16 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_OPERATION </span> </td> 
   <td colname="col3"> Operation is not supported. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 17 </td> 
   <td colname="col2"><span class="codeph"> WAITING_FOR_INIT </span> </td> 
   <td colname="col3"> Not yet initialized. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 18 </td> 
   <td colname="col2"><span class="codeph"> INVALID_PARAMETER </span> </td> 
   <td colname="col3"> Invalid parameter. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 19 </td> 
   <td colname="col2"><span class="codeph"> INVALID_OPERATION</span> </td> 
   <td colname="col3"> Operation not permitted. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 20 </td> 
   <td colname="col2"><span class="codeph"> OP_ONLY_ALLOWED_IN_PAUSED_STATE</span> </td> 
   <td colname="col3"> The operation is allowed only while paused. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 21 </td> 
   <td colname="col2"><span class="codeph"> OP_INVALID_WITH_AUDIO_ONLY_FILE</span> </td> 
   <td colname="col3"> Operation cannot be used on audio only files. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 22 </td> 
   <td colname="col2"><span class="codeph"> PREVIOUS_STEP_SEEK_IN_PROGRESS</span> </td> 
   <td colname="col3"> Previous seek operation is still in progress. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 23 </td> 
   <td colname="col2"><span class="codeph"> SOURCE_NOT_SPECIFIED </span> </td> 
   <td colname="col3"> Resource not specified. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 24 </td> 
   <td colname="col2"><span class="codeph"> RANGE_ERROR</span> </td> 
   <td colname="col3"> Specified value is out of range. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 25 </td> 
   <td colname="col2"><span class="codeph"> INVALID_SEEK_TIME</span> </td> 
   <td colname="col3"> Invalid seek time. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 26 </td> 
   <td colname="col2"><span class="codeph"> FILE_STRUCTURE_INVALID</span> </td> 
   <td colname="col3"> The file specified does not conform to the expected syntax. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 27 </td> 
   <td colname="col2"><span class="codeph"> COMPONENT_CREATION_FAILURE</span> </td> 
   <td colname="col3"> An essential component could not be created. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 28 </td> 
   <td colname="col2"><span class="codeph"> DRM_INIT_ERROR</span> </td> 
   <td colname="col3"> Failed to create DRM context. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 29 </td> 
   <td colname="col2"><span class="codeph"> CONTAINER_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> Container type is not supported. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 30 </td> 
   <td colname="col2"><span class="codeph"> SEEK_FAILED</span> </td> 
   <td colname="col3"> Seek failed. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 31 </td> 
   <td colname="col2"><span class="codeph"> CODEC_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Unsupported codec. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 32 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_UNAVAILABLE</span> </td> 
   <td colname="col3"> Network is not available. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 33 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_ERROR</span> </td> 
   <td colname="col3"> Error getting data from the Network. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 34 </td> 
   <td colname="col2"><span class="codeph"> OVERFLOW</span> </td> 
   <td colname="col3"> Overflow. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 35 </td> 
   <td colname="col2"><span class="codeph"> VIDEO_PROFILE_NOT_SUPPORTED</span> </td> 
   <td colname="col3"> Unsupported video profile. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 36 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_NOT_LOADED</span> </td> 
   <td colname="col3"> An operation was attempted on a HOLD period or a period that has not yet been loaded. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 37 </td> 
   <td colname="col2"><span class="codeph"> INVALID_REPLACE_DURATION</span> </td> 
   <td colname="col3"> The replace duration specified is invalid or extends past the end of the stream. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 38 </td> 
   <td colname="col2"><span class="codeph"> CALLED_FROM_WRONG_THREAD</span> </td> 
   <td colname="col3"> API can't be called from the wrong thread. Mostly, for API elements that should be called from Main thread only. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 39 </td> 
   <td colname="col2"><span class="codeph"> FRAGMENT_READ_ERROR</span> </td> 
   <td colname="col3"> Fragment read error. No failover present. Engine will try to read the next fragment. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 40 </td> 
   <td colname="col2"><span class="codeph"> ABORTED</span> </td> 
   <td colname="col3"> The operation was aborted by an explicit Abort or Destroy call. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 41 </td> 
   <td colname="col2"><span class="codeph"> UNSUPPORTED_HLS_VERSION</span> </td> 
   <td colname="col3"> Cannot play this version of HLS media. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 42 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_FAIL_OVER</span> </td> 
   <td colname="col3"> Cannot fail over. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 43 </td> 
   <td colname="col2"><span class="codeph"> HTTP_TIME_OUT</span> </td> 
   <td colname="col3"> HTTP download has timed out. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 44 </td> 
   <td colname="col2"><span class="codeph"> NETWORK_DOWN </span> </td> 
   <td colname="col3"> The user's network connection is down. Playback could stop any moment and will resume when the connection is available. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 45 </td> 
   <td colname="col2"><span class="codeph"> NO_USABLE_BITRATE_PROFILE</span> </td> 
   <td colname="col3"> No usable bit rate profile found in the stream. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 46 </td> 
   <td colname="col2"><span class="codeph"> BAD_MANIFEST_SIGNATURE</span> </td> 
   <td colname="col3"> The manifest has a bad signature. It failed the manifest signing test. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 47 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_LOAD_PLAYLIST</span> </td> 
   <td colname="col3"> Cannot load a playlist. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 48 </td> 
   <td colname="col2"><span class="codeph"> REPLACEMENT_FAILED</span> </td> 
   <td colname="col3"> Replacement specified in an Insert API could not succeed. This means that the insertion succeeded but replacement did not. Replacement could fail if the manifest to be replaced has been removed from the timeline. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 49 </td> 
   <td colname="col2"><span class="codeph"> SWITCH_TO_ASYMMETRIC_PROFILE</span> </td> 
   <td colname="col3"> DRM is switching to an asymmetric profile. All the profiles are expected to be aligned in duration. If not, this warning will be thrown, and there may be jumps in the playback. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 50 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_BACKWARD</span> </td> 
   <td colname="col3"> Live window is expected to move forward only. If not, this warning will be thrown, and the window will not be read. Because of that, there may be jumps (or stop / long pause) in the playback. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 51 </td> 
   <td colname="col2"><span class="codeph"> CURRENT_PERIOD_EXPIRED</span> </td> 
   <td colname="col3"> Live window moved beyond the current period. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 52 </td> 
   <td colname="col2"><span class="codeph"> CONTENT_LENGTH_MISMATCH</span> </td> 
   <td colname="col3"> The content-length reported by the HTTP server did not match the actual media size. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 53 </td> 
   <td colname="col2"><span class="codeph"> PERIOD_HOLD</span> </td> 
   <td colname="col3"> The media reader is unable to read further because it has reached the time set by setHoldAt API. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 54 </td> 
   <td colname="col2"><span class="codeph"> LIVE_HOLD </span> </td> 
   <td colname="col3">The media reader is unable to load segments because it has reached the end of the live window. Segment loading will resume when the server ads new media to the live window. This state is usually reached if: 
    <ul id="ul_FCFF658EDA4144E59970B317D6DEB624"> 
     <li id="li_2F6EEEB782D54CD999BC7CC7C0B78B48">The <span class="codeph"> bufferTime</span> is too high (equal to or higher than the live window duration). </li> 
     <li id="li_25CE97115ED64E44AA89977FB5F0DCF7">A combination of one or more of insert/erase API replaced more media than it added. </li> 
     <li id="li_1B14716B2157492AB1859306D1250523">The next period is a live period with a pending media replacement (due to InsertBy API call) </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 55 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_INTERLEAVING </span> </td> 
   <td colname="col3"> The audio and video interleaving in the media is not done properly. This is a packaging error. The warning is dispatched when the difference exceeds two seconds. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 56 </td> 
   <td colname="col2"><span class="codeph"> DRM_NOT_AVAILABLE</span> </td> 
   <td colname="col3"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 57 </td> 
   <td colname="col2"><span class="codeph"> PLAYBACK_NOT_AUTHORIZED</span> </td> 
   <td colname="col3"> HLS playback has not been enabled in the Flash Player. See AuthorizedFeatures.enableHLSPlayback. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 58 </td> 
   <td colname="col2"><span class="codeph"> BAD_MEDIA_SAMPLE_FOUND</span> </td> 
   <td colname="col3"> The decoder received a bad sample that cannot be decoded. This is usually not a fatal error but indicates that there may be glitches in the audio/video. Too many instances of this error indicate a bad encoding or bad file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 59 </td> 
   <td colname="col2"><span class="codeph"> RANGE_SPANS_READ_HEAD</span> </td> 
   <td colname="col3"> After playback has started, the Insert/Replace range should not contain the read head. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 60 </td> 
   <td colname="col2"><span class="codeph"> POSTROLL_WITH_LIVE_NOT_ALLOWED</span> </td> 
   <td colname="col3"> Post-roll insertions are not allowed on a live media. They are, however, allowed after the server marks the media as complete. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 61 </td> 
   <td colname="col2"><span class="codeph"> INTERNAL_ERROR</span> </td> 
   <td colname="col3"> A very rare issue that should never happen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 62 </td> 
   <td colname="col2"><span class="codeph"> SPS_PPS_FOUND_OUTSIDE_AVCC</span> </td> 
   <td colname="col3"> The stream does not follow the packaging recommendation of always putting H264 SPS/PPS in an AVCC. Seek / playback issues might be seen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 63 </td> 
   <td colname="col2"><span class="codeph"> PARTIAL_REPLACEMENT</span> </td> 
   <td colname="col3"> Replacement specified in an Insert API was only partially done. This happens when replaceDuration spans over the timeline duration. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 64 </td> 
   <td colname="col2"><span class="codeph"> RENDITION_M3U8_ERROR</span> </td> 
   <td colname="col3"> Rendition playlist had an error loading. This is only for AVE, not for FlashPlayer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 65 </td> 
   <td colname="col2"><span class="codeph"> NULL_OPERATION</span> </td> 
   <td colname="col3"> Operation does not do anything. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 66 </td> 
   <td colname="col2"><span class="codeph"> SEGMENT_SKIPPED_ON_FAILURE</span> </td> 
   <td colname="col3"> Segment cannot be played and is skipped on failure. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 67 </td> 
   <td colname="col2"><span class="codeph"> INCOMPATIBLE_RENDER_MODE</span> </td> 
   <td colname="col3"> Incompatible render mode. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 68 </td> 
   <td colname="col2"><span class="codeph"> PROTOCOL_NOT_SUPPORTED </span> </td> 
   <td colname="col3"> The Web protocol used in the URL is not supported. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 69 </td> 
   <td colname="col2"><span class="codeph"> PARSE_ERROR_INCOMPATIBLE_VERSION</span> </td> 
   <td colname="col3"> Error while parsing media file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 70 </td> 
   <td colname="col2"><span class="codeph"> MANIFEST_FILE_UNEXPECTEDLY_CHANGED</span> </td> 
   <td colname="col3"> Manifest file was changed in an unexpected manner. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 71 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_SPLIT_TIMELINE</span> </td> 
   <td colname="col3"> Cannot perform a split operation on a timeline. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 72 </td> 
   <td colname="col2"><span class="codeph"> CANNOT_ERASE_TIMELINE</span> </td> 
   <td colname="col3"> Cannot perform an erase operation on a timeline. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 73 </td> 
   <td colname="col2"><span class="codeph"> DID_NOT_GET_NEXT_FRAGMENT</span> </td> 
   <td colname="col3"> Did not get the next fragment. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 74 </td> 
   <td colname="col2"><span class="codeph"> NO_TIMELINE</span> </td> 
   <td colname="col3"> No timeline present in an internal data structure. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 75 </td> 
   <td colname="col2"><span class="codeph"> LISTENER_NOT_FOUND</span> </td> 
   <td colname="col3"> No listener found in an internal data structure. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 76 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_START_ERROR</span> </td> 
   <td colname="col3"> Unable to start audio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 77 </td> 
   <td colname="col2"><span class="codeph"> NO_AUDIO_SINK</span> </td> 
   <td colname="col3"> No audio sink present in an internal data structure. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 78 </td> 
   <td colname="col2"><span class="codeph"> FILE_OPEN_ERROR</span> </td> 
   <td colname="col3"> Unable to open file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 79 </td> 
   <td colname="col2"><span class="codeph"> FILE_WRITE_ERROR</span> </td> 
   <td colname="col3"> Unable to write to a file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 80 </td> 
   <td colname="col2"><span class="codeph"> FILE_READ_ERROR</span> </td> 
   <td colname="col3"> Unable to read from a file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 81 </td> 
   <td colname="col2"><span class="codeph"> ID3PARSE_ERROR</span> </td> 
   <td colname="col3"> There was an error parsing ID3 data. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 82 </td> 
   <td colname="col2"><span class="codeph"> SECURITY_ERROR </span> </td> 
   <td colname="col3"> Loading the content failed because of security restrictions. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 83 </td> 
   <td colname="col2"><span class="codeph"> TIMELINE_TOO_SHORT</span> </td> 
   <td colname="col3"> The timeline duration is too short. If this is a live stream, frequent buffering may happen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 84 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_START</span> </td> 
   <td colname="col3"> The stream has been switched to an audio-only stream. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 85 </td> 
   <td colname="col2"><span class="codeph"> AUDIO_ONLY_STREAM_END</span> </td> 
   <td colname="col3"> The stream has been switched from audio-only to a stream with video. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 87 </td> 
   <td colname="col2"><span class="codeph"> KEY_NOT_FOUND </span> </td> 
   <td colname="col3"> Key cannot be found. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 88 </td> 
   <td colname="col2"><span class="codeph"> INVALID_KEY</span> </td> 
   <td colname="col3"> The key is invalid. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 89 </td> 
   <td colname="col2"> <span class="codeph"> KEY_SERVER_NOT_FOUND</span> </td> 
   <td colname="col3"> Key server does not return a key. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 90 </td> 
   <td colname="col2"> <span class="codeph"> MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</span> </td> 
   <td colname="col3"> Cannot handle main manifest update. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 91 </td> 
   <td colname="col2"> <span class="codeph"> UNREPORTED_TIME_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Unreported time (PTS) discontinuity found. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 92 </td> 
   <td colname="col2"> <span class="codeph"> UNMATCHED_AV_DISCONTINUITY_FOUND</span> </td> 
   <td colname="col3"> Unmatched Audio and Video discontinuity found. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 93 </td> 
   <td colname="col2"><span class="codeph"> TRICKPLAY_ENDED_DUE_TO_ERROR</span> </td> 
   <td colname="col3">There was an error while playing media in <i>trick play</i> mode. Trick play mode is ended and the stream is paused. Call <span class="codeph"> Play()</span> to play the media in normal mode. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 95 </td> 
   <td colname="col2"><span class="codeph"> LIVE_WINDOW_MOVED_AHEAD</span> </td> 
   <td colname="col3"> The player is out of the live window and must seek forward to catch up. </td> 
  </tr> 
 </tbody> 
</table>

## NATIVE_ERROR: Crypto values {#section_39365E545CAC49B9A4D4678657BB2155}

The crypto module of the Adobe video engine returns these notifications in the `NATIVE_ERROR` metadata object. 

|  Value for NATIVE_ERROR_CODE metadata key  | Value for NATIVE_ERROR_NAME metadata key  | Meaning  |
|---|---|---|
|  300  | `CRYPTO_ALGORITHM_NOT_SUPPORTED`  | Algorithm being used is not supported.  |
|  301  | `CRYPTO_ERROR_CORRUPTED_DATA`  | Data is corrupted.  |
|  302  | `CRYPTO_ERROR_BUFFER_TOO_SMALL`  | Buffer too small.  |
|  303  | `CRYPTO_ERROR_BAD_CERTIFICATE`  | Bad certificate.  |
|  304  | `CRYPTO_ERROR_DIGEST_UPDATE`  | Digest update.  |
|  305  | `CRYPTO_ERROR_DIGEST_FINISH`  | Digest finish.  |
|  306  | `CRYPTO_ERROR_BAD_PARAMETER`  | Bad parameter.  |
