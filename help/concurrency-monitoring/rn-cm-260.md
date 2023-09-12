---
title: Adobe Primetime Concurrency Monitoring 2.6.0 Release Notes
description: Adobe Primetime Concurrency Monitoring 2.6.0 Release Notes
---

# Adobe Primetime Concurrency Monitoring 2.6.0 Release Notes {#cm-260}
 

This page describes new features, changes, and known issues with this release:

 

## Release Date: 11/10/2016

 

## New Features

This release adds the ability to terminate existing stream(s) in order to allow the current stream to start (a.k.a. kill stream).

 

**Remote termination**

* On a 409 Conflict response, each session listed within "conflicts" field of the advice will carry a terminationCode attribute.
* The user can be prompted with the list of conflicting sessions and be allowed to choose the one(s) to kill
* Remote sessions can only be killed by passing an X-Terminate request header (with the selected termination codes as values) within a session init attempt.
* A new type of "advice" was defined for the 410 Gone response to indicate the session that has killed the current one.
 

See the updated documentation for more details.

 

>[!NOTE]
>
>The session definition used for listing active sessions was updated to include application name and device name (instead of the application ID).


 

## Bug Fixes {#bug-fixes}

Removed duplicate headers in server response (the fix involves both CORS headers and the Date one).
 

 

## Known Issues {#known-issues}

N/A
