---
title: How to migrate the MVPD Login Page from iFrame to Popup
description: How to migrate the MVPD Login Page from iFrame to Popup
exl-id: 389ea0ea-4e18-4c2e-a527-c84bffd808b4
---
# (Legacy) How to migrate the MVPD login page from iFrame to Popup {#migr-mvpd-login-iframe-popup}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

## Popup versus iFrame {#popup-vs-iframe}

Some users have encountered 3rd-party cookie issues with the iFrame implementation of an MVPD login page. 
<!--These issues are described in the tech notes linked below:

* [Adobe Pass Authentication and Safari login issues](https://tve.helpdocsonline.com/adobe-pass)
* [MVPD iFrame login and 3rd party cookies](https://tve.helpdocsonline.com/mvpd)-->

The Adobe Pass Authentication team **recommends implementing the popup / new window login page** rather than the iFrame version on Firefox and Safari.  However, if you are implementing a login page for Internet Explorer, you may encounter issues with the popup implementation. The IE issues are caused by the fact that, after the user authenticates with their MVPD in the popup window, Adobe Pass Authentication forces a parent page redirect, which is seen as a popup blocker by Internet Explorer. The Adobe Pass Authentication team **recommends implementing the iFrame login for Internet Explorer**.

The sample code presented in this tech note uses a hybrid implementation of both iFrame and popup - opening an iFrame on Internet Explorer and a popup on the other browsers. 

Considering that an iFrame implementation already exists, the first part of the tech note presents the code for the iFrame implementation and the second part presents the changes to accommodate the popup implementation as the default.


## MVPD picker with login page in an iFrame {#mvpd-pickr-iframe}

Previous code examples showed an HTML page that contains the &lt;div&gt; tag where the iFrame is to be created along with the close iFrame button:

```HTML
<body> 
    <div id="mvpddiv">
        <div style="background: red">
            <input type="button" id="btnCloseIframe" value="X" onclick="closeIframeAction();">
        </div>
        <br/>
        <!-- We use the "about:blank" value so that when the iFrame loads
             we do not see the the parent page. -->
        <iframe id="mvpdframe" name="mvpdframe" src="about:blank"></iframe>
    </div> 
</body>
```

Here is the associated **JavaScript** code:

```JavaScript
/*
 * Callback indicating that the AccessEnabler swf has initialized
 */
function swfLoaded() {
    // AccessEnabler is loaded so we can use the API function it provides
    accessEnablerObject.setRequestor(requestorID); 
    accessEnablerObject.checkAuthentication();
} 
/*
* The code the correctly closes the opened IFrame and does not leave the
* AccessEnabler in an undefined state.
*/
function closeIframeAction () {
    accessEnablerObject.setSelectedProvider(null);
    /* We use the "about:blank" value so that when the iFrame loads
     * we do not see the the previous MVPD.
     */
    document.getElementById('mvpdframe').src="about:blank";
    document.getElementById('mvpddiv').style.visibility="hidden";
    document.getElementById('mvpddiv').style.display="none";
}
/*
* Some of the supported MVPDs require their login pages to be displayed within an iFrame.
* In your HTML page, you must include the following <div> tag: "<div id="mvpddiv"></div>".
* Called when the selected MVPD requires an iFrame in which to display its authentication UI.
*/
function createIFrame(inWidth, inHeight) {
     // Create the iFrame to the specified width and height for the auth page
    ifrm = document.createElement("IFRAME");
    ifrm.name = "mvpdframe";
    ...
    document.getElementById('mvpddiv').appendChild(ifrm);
    ...
    // Force the name into the DOM since it is still not refreshed, for IE
    window.frames["mvpdframe"].name = "mvpdframe";
}
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
    /* This is an example how previously the MVPD picker was build and will be replaced. */
}
/* 
* Sending the user selected MVPD of the custom dialog is achieved
* by calling the API function setSelectedProvider(providerID:String).
*/
function setSelectedProvider(providerID) {
    accessEnablerObject.setSelectedProvider(providerID);
}

```


## MVPD picker with login page in a popup window {#mvpd-pickr-popup}

Since we won't be using an **iFrame** anymore, the HTML code will not contain the iFrame or the button to close the iFrame. The div that formerly contained the iFrame - **mvpddiv** - will be kept and used for the following:

* to notify the user that the MVPD login page is already open if the popup focus is lost
* to provide a link to regain focus on the popup

```HTML
<body onload="javascript:loadAccessEnabler();"> 
   <div id="aeHolder">
       <div name="contentAccessEnabler" id="contentAccessEnabler"></div>
   </div>
   <div id="mvpddiv">
      <p>
      <strong>No login window?</strong>
      <br/>
      <a href="javascript:mvpdWindow.focus();">Click here to open it.</a>
      <br/>
      Still not working? Check popup blockers!
      </p>
   </div> 
 
   <div id="picker" style="display:none">
      Choose MVPD: <br/>
      <select id="mvpdList" multiple></select>
      <br/>
         <a id="authenticateButton" onclick="javascript:authenticate();">Authenticate</a>
   </div>
</body>
```

The list of MVPDs will be displayed in the div called **picker** as a select **-mvpdList**.

A new API callback will be used - **setConfig(configXML)**. The callback is triggered after calling the setRequestor(requestorID) function. This callback returns the list of MVPDs that are integrated with the requestorID previously set. In the callback method, the incoming XML will be parsed, and the list of MVPDs cached. The MVPD picker is also created but not displayed.

```JavaScript
var mvpdList;  // The list of cached MVPDs
var mvpdWindow;  // The reference to the popup with the MVPD login page
var cancelTimer = 0;
/* Callback indicating that the AccessEnabler swf has initialized */
function swfLoaded() {
   accessEnablerObject = $('#AccessEnabler').get(0);
   // Using a custom implementation of the MVPD picker
   accessEnablerObject.setProviderDialogURL('none');
   accessEnablerObject.setRequestor(requestorID); 
}

function setConfig(configXML) {
   mvpdList = [];
   $.each($($.parseXML(configXML)).find('mvpd'), function (idx, item) {
      var mvpdId = $(item).find('id').text();
      mvpdList[mvpdId] = {
         displayName: $(item).find('displayName').text(),
         logo: $(item).find('logoUrl').text(),
         popup: $(item).find('iFrameRequired').text() == "true",
         width: $(item).find('iFrameWidth').text(),
         height: $(item).find('iFrameHeight').text()
      };

      $('#mvpdList').append($('<option value="' + mvpdId + '" title="' + mvpdId + '">' + mvpdList[mvpdId].displayName + '</option>'));
   });
   accessEnablerObject.getAuthentication();
}
```

After the getAuthentication() or getAuthorization() function is called, the displayProviderDialog() callback is triggered. Normally, inside this callback, the MVPD list would have been built and displayed. Since the MVPD picker is already built, the only thing left to do is to display it to the user.

```JavaScript
/*
 * The custom non-Flash MVPD selector dialog will be implemented in this function.
 */
function displayProviderDialog(providers) {
   $('#picker').show();
}
```

After the user has selected an MVPD from the picker, the popup needs to be created. Some browsers may block the popup if it is created with about:blank or with a page that is on another domain - therefore it is recommended to open it with the hostname from where the AccessEnabler is loaded.

In the iFrame implementation, reseting the authentication flow was being done by the btnCloseIframe button and the JavaScript function closeIframeAction(), but now decorating the iFrame is not possible anymore. So, the same behavior is achieved by watching for when the popup is closed (either by the user or by finishing the authentication flow). A snippet of code has been added that also helps in case the user loses focus of the popup: 

```HTML
"<a href="javascript:mvpdWindow.focus();">Click here to open it.</a>".
```

On the createIFrame() callback the **mvpddiv** div will be shown.

```JavaScript
function createIFrame(width, height) {
   $('#mvpddiv').show();
   if (useIframeLoginStyle) {
      ...
   }
}

/* Function called when user has selected the MVPD from the picker */
function authenticate() {
   var selectedMvpd = $('#mvpdList').val()[0];
   if (mvpdList[selectedMvpd].popup) {
      mvpdWindow = window.open("http://entitlement.auth-staging.adobe.com", "mvpdframe", "width=" + mvpdList[selectedMvpd].width + ",height=" + mvpdList[selectedMvpd].height, true);
      if (!mvpdWindow) {
         // Message to user that popup blocker is not allowing the authentication process to start
      }
      //watch the mvpd popup for close
      clearInterval(cancelTimer);
      cancelTimer = setInterval(checkClosed, 200);
   }
   accessEnablerObject.setSelectedProvider(selectedMvpd);
}

function checkClosed() {
   try {
      if (mvpdWindow && mvpdWindow["closed"]) {
         clearInterval(cancelTimer);
         accessEnablerObject.setSelectedProvider(null);
         accessEnablerObject.getAuthentication();
         $('#mvpddiv').hide();
      }
   } catch (error) {
      console.log(error);
   }
}
```

>[!IMPORTANT]
>
>* The sample code contains a hardcoded variable for the used requestorID - 'REF' which should be replaced by a real programmer requestor id.
>* The sample code will only run properly from a whitelisted domain associated to the used requestor id.
>* Since the entire code is available for download, the code presented in this tech note has been truncated. For a complete sample, see **JS iFrame vs Popup Sample**.
>* The external JavaScript libraries were linked from [Google Hosted Services](https://developers.google.com/speed/libraries/).
