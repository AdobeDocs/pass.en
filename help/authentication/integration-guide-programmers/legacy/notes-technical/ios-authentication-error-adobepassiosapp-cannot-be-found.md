---
title: iOS Authentication Error - adobepass.ios.app Cannot Be Found
description: iOS Authentication Error - adobepass.ios.app Cannot Be Found
exl-id: cd97c6fb-f0fa-45c2-82c1-f28aa6b2fd12
---
# (Legacy) iOS Authentication Error - adobepass.ios.app Cannot Be Found {#ios-authentication-error-adobepass.ios.app-cannot-be-found}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

## Issue {#issue}

The user is going through the Authentication flow, and after they successfully entered their credentials with their provider they get redirected back to either an error page, a search page, or some other custom page informing them that `adobepass.ios.app` could not be found/resolved.

## Explanation {#explanation}

On iOS, `adobepass.ios.app` is used as the final redirection URL to indicate that the AuthN flow is complete. At this point the app needs to make a request to the AccessEnabler to get the AuthN Token and to finalize the AuthN flow.

The problem is that `adobepass.ios.app` doesn't actually exist and will trigger an error message in the `webView`. Older versions of the iOS DemoApp assumed that this error would always be triggered at the end of the AuthN flow, and was set up to handle it accordingly (`indidFailLoadWithError`).

**Note:** This issue has been fixed in later versions of the DemoApp (included with the iOS SDK download).

Unfortunately, this assumption is NOT correct. There are some so-called "smart" DNS or Proxy servers that won't simply pass-on the raised error, but will instead do one of the following: 

- Create a custom error page
- Forward to a search page, or some other type of customer page or portal.

In those cases, the response that comes back to the iOS webView will be a perfectly valid response as far as the webView is concerned, and will NOT trigger the error that the old DemoApp was depending on.

## Solution {#solution}

Do NOT make the same assumption that the DemoApp makes. Instead, intercept the request before it is executed (in `shouldStartLoadWithRequest`) and handle it appropriately.

Example of how to intercept the request before it is executed:

```obj-c
- (BOOL)webView:(UIWebView*)localWebView shouldStartLoadWithRequest:(NSURLRequest*)request navigationType:(UIWebViewNavigationType)navigationType {

NSString *absolutePath = [[request URL] absoluteString]; 
if ([absolutePath isEqualToString:ADOBEPASS_REDIRECT_URL] && ![APP_DELEGATE getAuthenticationWasCalled]) {

// user was logged ok => call getAuthenticationToken() 
[APP_DELEGATE setGetAuthenticationWasCalled:YES]; 
[[APP_DELEGATE accessEnabler] getAuthenticationToken];
return NO;

}

return YES;

}
```

A few things to note:

- NEVER use `adobepass.ios.app` directly anywhere in the code. Instead use the constant `ADOBEPASS_REDIRECT_URL`
- The `return NO;` statement will prevent the page from loading
- Make absolutely sure that the `getAuthenticationToken` call is called once and only once in your code. Multiple calls to `getAuthenticationToken` will result in undefined results.
