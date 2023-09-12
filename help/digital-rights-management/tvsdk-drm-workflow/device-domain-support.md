---
description: Typically, all Primetime DRM licenses, at creation time, are bound to a unique device. This binding prevents users from sharing licenses across different devices without authorization. In addition to per-device binding, Primetime DRM provides the ability to bind licenses to a Device Domain, or group of devices.
title: Play encrypted content using domain support
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
---
# Device domain support {#device-domain-support}

Typically, all Primetime DRM licenses, at creation time, are bound to a unique device. This binding prevents users from sharing licenses across different devices without authorization. In addition to per-device binding, Primetime DRM provides the ability to bind licenses to a Device Domain, or group of devices.

If the content metadata specifies that device domain registration is required, the application can invoke an API to join a device group. This action triggers a domain registration request to be sent to the domain server. Once a license is issued to a device group, the license can be exported and shared with other devices that have joined the device group.

The device group information is then used in the `DRMContentData` `VoucherAccessInfo` object, which will then be used to present the information that is required to successfully retrieve and consume a license.

## Play encrypted content using domain support {#play-encrypted-content-using-domain-support}

To play encrypted content using Primetime DRM , perform the following steps: 

1. Using `VoucherAccessInfo.deviceGroup`, check if device group registration is required.
1. If authentication is required:
   1. Use the `DeviceGroupInfo.authenticationMethod` property find out if authentication is required.
   1. If authentication is required, authenticate the user by performing ONE of the following steps:

       * Obtain the user's username and password and invoke `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`. 
       * Obtain a cached/pre-generated authentication token and invoke `DRMManager.setAuthenticationToken()`.

   1. Invoke `DRMManager.addToDeviceGroup()`
1. Get the license for the content by performing one of the following tasks:
   1. Use the `DRMManager.loadVoucher()` method.
   1. Obtain the license from a different device registered in the same device group, and provide the license to the `DRMManager` through the `DRMManager.storeVoucher()` method.
1. Play the encrypted content using the `Primetime.play()` method.
To export the license for the content, any of the devices can provide the license's raw bytes using the `DRMVoucher.toByteArray()` method after obtaining the license from the Primetime DRM license server. Content providers typically limit the number of devices in a device group. If the limit is reached, you may need to call the `DRMManager.removeFromDeviceGroup()` method on an unused device before registering the current device.
