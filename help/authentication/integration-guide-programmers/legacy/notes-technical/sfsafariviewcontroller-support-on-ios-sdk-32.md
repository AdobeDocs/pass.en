---
title: SFSafariViewController support on iOS SDK 3.2+
description: SFSafariViewController support on iOS SDK 3.2+
exl-id: 6691550f-c36f-4fae-aa77-082ca7d8a60a
---
# (Legacy) SFSafariViewController support on iOS SDK 3.2+ {#sfsafariviewcontroller-support-on-ios-sdk-3.2}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>


**Due to security requirements, some MVPD's login pages MUST be presented in a SFSafariViewController, instead of web views.**

Some MVPD's require that their login pages be presented in a secure browser control like SFSafariViewController. They are activelly blocking webviews, so in order to be able to authenticate with them we must use SVC. 

## Compatibility {#compatiblity}

Starting with iOS SDK version 3.1, the AccessEnabler SDK automatically displays the login page for specific MVPD's in a SFSafariViewController, based on server configuration.

Version 3.1 of the SDK automatically presents the SFSafariViewController from application's root view controller. While this simplifies login page management for implementors, there are cases where presenting the SFSafariViewController from root view controller is not possible, due to app's specifice implementation (like a modal controller already visible).

For such cases, the 3.2 version introduces the abbility for the programmer to manually manage the SVC.

## Manual SVC management {#manual-svc-management}

In order to manually manage SVC the implementor must perform the following steps:
 

1.  call **setOptions(["handleSVC":true])** after AccessEnabler initialization (make sure this call is performed before authentication begins). This will enable "manual" SVC management, the SDK will not automatically present the SVC, but instead, when needed will     call **navigate(toUrl:*{url}* useSVC:true)**.  

1.  implement the optional callback **`navigateToUrl:useSVC:`** inside the implementation you must create a svc instance using the SFSafariViewController instance using the provided url, and present it on the screen:

    ```obj-c    
    func navigate(toUrl url: String!, useSVC: Bool) {
        svc =  SFSafariViewController(url: URL(string: url)!)
        svc.delegate = self
        myController.present(svc, animated: true)
        }
    ```    
      
    ***Notes:***
    
      - *You can customize the SFSafariViewController any way you want. For example on iOS 11+ you can change the "Done" label to "Cancel".*
      - *in order to be able to dismiss the svc, you need a reference to it, please do not create it in the scope of **navigateToUrl:useSVC***
      - *use your own view controller for "myController"*  
         

1.  In your application's delegate implementation of **application(\_app: UIApplication, open url: URL, options: \[UIApplicationOpenURLOptionsKey: Any\]) -\> Bool**, add code to close the svc. You should already have some code there that calls **accessEnabler.handleExternalURL()**. Just below add:

    ```obj-c    
    if(svc != nil) {
        svc.dismiss(animated: true)
    }
    ```

    Again, svc is a reference to the SFSafariViewController you created at step 2.  
     

1.  Implement **safariViewControllerDidFinish(\_ controller: SFSafariViewController)** from **SFSafariViewControllerDelegate** in order to catch when the user cancelled the svc using the "Done" button. In this function, in order to inform the SDK that authentication has been canceled you need to call:
    
    ```obj-c 
    accessEnabler.setSelectedProvider(nil)
    ```
