---
title: Using the DRMManager class overview
description: Using the DRMManager class overview
copied-description: yes
---

# Using the DRMManager class {#using-the-drmmanager-class}

Use the `DRMManager` class to manage licenses and Primetime DRM license server sessions in applications.

**License management**

Whenever a device plays protected content, the runtime obtains and caches the license required to view the content. If the application saves the content locally, and the license allows offline playback, the user can view the content in the application without a network connection. Using the `DRMManager`, you can pre-cache the license. The application does not have to obtain the license necessary to view the content. For example, your application could download the media file and then obtain the license while the user is still online.

To preload a license, use a `DRMContentData` object. The `DRMContentData` object contains the URL of the Primetime DRM license server that can provide the license and describes whether user authentication is required. With this information, you can call the `DRMManager` `loadVoucher()` method to obtain and cache the license. The workflow for pre-loading licenses is described in more detail in *Pre-loading licenses for offline playback*.

**Session management**

You can also use the `DRMManager` to authenticate the user to a Primetime DRM license server and to manage persistent sessions. Call the `DRMManager` `authenticate()` method to establish a session with the Primetime DRM license server. When authentication is completed successfully, the `DRMManager` dispatches a `DRMAuthenticationCompleteEvent` object. This object contains a session token. You can save this token to establish future sessions so that the user does not have to provide their account credentials. Pass the token to the `setAuthenticationToken()` method to establish a new authenticated session. (The settings of the server that generated the token determine the token expiration and other attributes).

## Handling DRMStatus Events {#handling-drmstatus-events}

The `DRMManager` dispatches a `DRMStatusEvent` object after a call to the `loadVoucher()` method completes successfully. If a license is obtained, then the detail property of the event object has the value: `DRM.voucherObtained`, and the voucher property contains the `DRMVoucher` object. If a license is not obtained, then the detail property still has the value: `DRM.voucherObtained`; however, the voucher property is null. A license cannot be obtained if, for example, you use the `LoadVoucherSetting` of `localOnly` and there is no locally cached license. If the `loadVoucher()` call does not complete successfully, perhaps because of an authentication or communication error, then the `DRMManager` dispatches a `DRMErrorEvent` or `DRMAuthenticationErrorEvent` object instead.

## Handling DRMAuthenticationComplete Events{#handling-drmauthenticationcomplete-events}

The `DRMManager` dispatches a `DRMAuthenticationCompleteEvent` object when a user is successfully authenticated through a call to the `authenticate()` method. The `DRMAuthenticationCompleteEvent` object contains a reusable token that can be used to persist user authentication across application sessions. Pass this token to `DRMManager` `setAuthenticationToken()` method to re-establish the session. (The token creator sets token attributes such as expiration. Adobe does not provide an API for examining token attributes.)

## Handling DRMAuthenticationError events{#handling-drmauthenticationerror-events}

The `DRMManager` dispatches a `DRMAuthenticationErrorEvent` object when a user cannot be successfully authenticated through a call to the `authenticate()` or `setAuthenticationToken()` methods.