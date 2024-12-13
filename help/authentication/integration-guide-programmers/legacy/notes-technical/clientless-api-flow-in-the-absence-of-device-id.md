---
title: Clientless API Flow in the Absence of Device ID
description: Clientless API Flow in the Absence of Device ID
exl-id: 6549a6d6-03a9-4d95-99fb-d3ada832323d
---
# (Legacy) Clientless API Flow in the Absence of Device ID {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>


## Issue

Not all smart device apps will be able to provide a unique Device ID.  Since deviceId is a mandatory parameter, the service returns a 400 error if it is not passed.


## Temporary Solution / Workaround

For clients with no Device ID:

1.  Call the registration code service the first time with `deviceId=dummy`
1.  From the response, extract the UUID. The UUID is available in the "id" element of the registration code response (XML and JSON response formats).
1.  Call the registration service a second time. This time, pass `deviceId=<uuid obtained in step #2>`
1.  Display the registration code obtained in Step 3 on the console UI


After these steps are done, Adobe Pass Authentication will use the UUID as the Device ID. Store this Device ID (UUID) in the local storage of the device. In the event that the user generates a new registration code, you should again run steps 1 through 4, and then replace the previously stored Device ID (UUID) with the new one.



## Permanent Solution

Adobe will change this in a future release, by making `deviceId` an optional payload when creating the reg code, and using UUID as the token key instead of `deviceId`, when `deviceId` is not present.

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->
