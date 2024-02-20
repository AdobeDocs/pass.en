---
title: Clientless API Implementation - Error codes / Messages With Probable Reason / Cause
description: Clientless API Implementation - Error codes / Messages With Probable Reason / Cause
exl-id: 616e35fc-9b72-422b-9a05-e6248bd52490
---
# Clientless API Implementation - Error codes / Messages With Probable Reason / Cause {#clientless-api-implementation--error-codes-messages-with-probable-reason-cause}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>


## Error: Not Authorized

### Causes:

1.  Missing authorization header in the POST
1.  Issue with authorization header - check if request time is in milliseconds.

## Error: SC 400 during authenticate

### Causes:

1.  The server did not find the registration code, which was created for a specific requestor and environment.
1.  You could be running into cross domain scripting issues
1.  Proper spoofing should be added to /etc/hosts file

## Error: 400 Bad Request

### Causes:

1.  Malformed url for POST/GET
1.  SAMLAssertionParserException – The encrypted SAML assertion could not be decrypted at Adobe's end

## Error: 403 Forbidden

### Causes:

1.  Too many rapid requests - a feature of the API management to prevent DoS attacks.
2.  If using prequal environment then add spoofing, otherwise make sure spoofing has been removed from /etc/hosts file

## Error: Unable to Login to MVPD page

### Causes:

1.  Username and password do not match 
2.  Login may have been disabled
3.  Check if the login is for production or staging


<!--

## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)

-->
