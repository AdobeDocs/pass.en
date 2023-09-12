---
title: Overview
description: Overview
copied-description: yes
exl-id: 7327386b-e796-4fa5-bda4-cacc612a9d1f
---
# Overview{#overview}

In order to issue licenses to clients, you must deploy an Adobe Access license server. The license server uses the Adobe® Access™ SDK to perform these tasks:

* Process authentication requests, if username/password authentication is supported. 
* Process license requests 
* Process Get Server Version requests -- All servers must implement support for this type of request. 
* Process domain registration requests -- Only needed if implementing a domain server. 
* Process domain de-registration requests -- Only needed if implementing a domain server. 
* Process synchronization -- Only needed if licenses specify Sync requirements.

In addition, the server needs to provide business logic for authenticating users, determining if users are authorized to view content, and optionally track license usage.

For details about the Java API discussed in this chapter, see *Adobe Access API Reference*.
