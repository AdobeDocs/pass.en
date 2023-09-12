---
title: Adobe Primetime Concurrency Monitoring 2.5.0 Release Notes
description: Adobe Primetime Concurrency Monitoring 2.5.0 Release Notes
---

# Adobe Primetime Concurrency Monitoring 2.5.0 Release Notes {#cm-250}
 
This page describes new features, changes, and known issues with this release:

Release Date: 04/21/2016

## New Features {#new-features}

The Concurrency Monitoring API v2.0 is now available in production. 

The V2 version unifies heartbeat and query calls and greatly simplifies the implementation when both these APIs are simultaneously used.

 

### Session lifecycle {#session-lifecycle}

* Write-only APIs for creation, keep-alive and termination of a session — i.e. no more queries, the decision is returned on both session init and heartbeat calls
* The heartbeat interval is now driven by the server via Expires headers set on both session init and keep-alive calls. This allows server side configuration of heartbeat intervals and one less harcoded value in the apps.
* The happy path (compliant behavior of both the user and the app) is "paved" with 2XX status codes

### Error handling {#error-handling}

* Deny decisions, missing metadata or application misbehavior are flagged as 4XX responses (Conflict, Bad Request, Unauthorized, Gone etc.)

* Whenever it makes sense, the response includes:

    * associated advice — detailed explanation(s) of the failure, to be prompted to the user.

    * obligations — mandatory actions that the application must take (e.g.: refresh metadata, logout from Adobe Pass).

### Metadata {#metadata}

* Standard instead of custom metadata - this allows the API to identify if wrong metadata is being sent or if metadata required by rules is missing.
* The required attributes for each application are now provided by an API call and should be cached by clients.
Notes

>[!NOTE]
>
>The V1 version continues to be available. If customers need to use queries outside of the heartbeat call the V1 version can be used.


 

### Bug Fixes {#bug-fixes}

N/A

### Known Issues {#known-issues}

N/A
