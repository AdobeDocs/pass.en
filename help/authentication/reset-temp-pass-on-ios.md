---
title: Reset Temp Pass on iOS
description: Reset Temp Pass on iOS
exl-id: 53a22fae-192c-4b4c-9d63-fd9a2d960923
---
# Reset Temp Pass on iOS {#reset-temp-pass-on-ios}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

The iOS Demo App includes a dedicated screen for resetting the Temp Pass TTL. The following information is required for the reset operation:

- **Environment:** specifies the Adobe Pay-TV pass server endpoint that will receive the reset Temp Pass network call. Possible values: **Prequal** (*mgmt-prequal.auth-staging.adobe.com*), **Release** (*mgmt.auth.adobe.com*) or **Custom** (reserved for Adobe internal testing).
- **OAuth2 Bearer Token:** the OAuth2 token is necessary for authorizing the Programmer for Adobe Pay-TV authentication. Such a token can be obtained from the dedicated Pay-TV authentication OAuth2 endpoint (e.g. *curl -u "\<consumer\_key\>:\<consumer\_secret\_key\>*" *"https://mgmt.auth.adobe.com/oauth2/permanent\_accesstoken?grant\_type=client\_credentials"*).
- **Requestor ID:** the unique ID for the current Programmer. This value is read from the main screen of the Demo App (the requestor field).
- **Temp Pass ID:** the unique ID for the Temp Pass MVPD.
- **Device ID:** hashed Device ID computed by the Demo App.
- **Generic Key:** some Temp Pass MVPDs (i.e. the next extensible Temp Pass functionality) support a generic key for resetting Temp Pass (alongside the Device ID).

All the above parameters (except the *Generic Key*) are mandatory. Here is an example of parameters and the associated network call that will be performed by the Demo App (the example is in the form of a *curl *command):

- **Environment:** Release (*mgmt.auth.adobe.com*)
- **OAuth2 Bearer Token:** H4j7cF3GtJX81BrsgDa10GwSizVz
- **Programmer ID:** REF
- **Temp Pass ID:** TempPassREF
- **Device ID:** f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991 
- **Generic Key:** null (no value provided)

```curl
curl -X DELETE -H "Authorization:Bearer* *H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset?device_id=f23804a37802993fdc8e28a7f244dfe088b6a9ea21457670728e6731fa639991&requestor_id=REF&mvpd_id=TempPassREF"
```

a DELETE HTTP request will be made to the **/reset** endpoint, passing the *OAuth2 Bearer Token* in the Authorization header and the *Device ID*, *Requestor ID* and *Temp Pass ID (MVPD ID)* as parameters.

If the Programmer supplies a value for the *Generic Key*, another HTTP call will be performed (this time to the **/reset/generic** endpoint), passing the *Generic Key* inside the *key* request parameter.

For example, setting the *Generic Key* to an E-mail address hash (for
Temp Pass MVPDs that support this kind of functionality) will yield the
following HTTP call (the E-mail is `user@domain.com` its SHA-256
hash is `f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7`):

```curl
curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz"
"https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=TempPassREF"
```

It's important to emphasize that resetting Temp Pass in the Demo App may not have the same effect for a Programmer app on the same device. This is due to the fact that the Device ID (as computed by the Demo App and the AccessEnabler) may not be the same for all applications on the device:

- iOS 6 and lower: the Device ID is computed using the MAC addres (which is unique per all apps), so resetting Temp Pass in the Demo App will reset it in all other Programmer apps on the device.

- iOS 7 and upper: the Device ID is computed based on the IDFV (ID for  Vendor) value, which is unique per all applications that have the same Bundle ID prefix (i.e. all components except the last). Since the Demo App and a Programmer app have different Bundle IDs, resetting Temp Pass in the Demo App will have no effect on a Programmer app.

The last use-case (iOS 7 and higher) is the most common so let's see how Programmers can reset Temp Pass for their apps in this situation. There are several options:

1.  Port the code from the Demo App to the Programmer app. The *TempPassResetViewController* and *DeviceIdDemoApp* classes contain the core logic for resetting Temp Pass, and they can easily be modified and included in the Programmer app.

1.  Execute the HTTP request for resetting Temp Pass with *curl*. The device\_Id parameter can be obtained by computing the IDFV of the Programmer app and applying a SHA-256 hash over it (sample code in the *DeviceIdDemoApp* class).

1.  Simply perform the reset from the Demo App by specifying the hashed IDFV of the Programmer's app as the *Generic Key*. This will result in two network calls: one for resetting Temp Pass for the Demo App (irrelevant to the Programmer) and one for resetting Temp Pass for the Programmer app.

All the above options are similar, it's up to the Programmer to choose one depending on the ease of implementation.
