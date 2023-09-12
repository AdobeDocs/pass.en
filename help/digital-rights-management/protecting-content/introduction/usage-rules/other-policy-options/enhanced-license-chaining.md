---
title: Enhanced license chaining
description: Enhanced license chaining
copied-description: yes
exl-id: 269e7866-fe43-45a8-84d8-c51e4fc95f77
---
# Enhanced license chaining {#enhanced-license-chaining}

You can use enhanced license chaining to update a license by using a parent root license for batch updating of licenses.

Primetime DRM 2.0 supports license chaining in which both the leaf and root licenses are bound to a specific machine. Primetime DRM 3.0 and higher has support for enhanced license chaining, in which a leaf is bound to a root license, and only the root license is bound to a specific machine or domain. The enhanced license chaining supports embedding a leaf license with the content, and the client only needs to acquire the root license from the license server in order to consume the protected content.

If you want to enable enhanced licence chaining, then you must assign a root encryption key to a Primetime DRM policy. The root encryption key is used to cryptographically bind the leaf license to the root license. 

>[!NOTE]
>
>Enhanced license chaining is supported by Primetime DRM clients version 3.0 or later. If an older client requests a license for content that supports the enhanced license chaining, the license server can still issue a license to this client by using the license chaining that is supported by Primetime DRM 2.0.

Example use case: Use this option to update any linked licenses by downloading a single root license. For example, implement subscription models where content can be played back as long as the user renews the subscription on a monthly basis. The benefit of this approach is that users only have to acquire a single license to update all of their subscription licenses.
