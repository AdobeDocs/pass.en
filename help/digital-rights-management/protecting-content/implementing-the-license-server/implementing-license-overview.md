---
title: License server overview
description: License server overview
copied-description: yes
exl-id: 101d9f63-b9b9-4281-a069-8c66427b34cb
---
# Overview {#license-server-overview}

Before you can issue licenses to clients, you must deploy an Adobe Primetime DRM license server. The license server uses the Primetime DRM SDK to perform a number of tasks.

To implement a License Server:

* Process authentication requests, if username/password authentication is supported. 
* Process license requests 
* Process Get Server Version requests—All servers must implement support for this type of request. 
* Process domain registration requests—Only needed if implementing a domain server. 
* Process domain de-registration requests—Only needed if implementing a domain server. 
* Process synchronization—Only needed if licenses specify Sync requirements.

In addition, the server needs to provide business logic for authenticating users, determining if users are authorized to view content, and optionally track license usage.

See *Adobe Primetime DRM API Reference* for details about the Java API.
