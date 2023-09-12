---
title: Enhanced license chaining
description: Enhanced license chaining
copied-description: yes
exl-id: 5553f055-903f-4140-a425-08f21e8bce87
---
# Enhanced license chaining {#enhanced-license-chaining}

Allows a license to be updated using a parent root license for batch updating of licenses.

Adobe Access 2.0 supported license chaining in which both the leaf and root licenses are bound to a specific machine. Adobe Access 3.0, has support for enhanced license chaining, in which a leaf is bound to a root license, and only the root license is bound to a specific machine or domain. The enhanced license chaining supports embedding leaf license with the content, and the client only needs to acquire the root license from the license server in order to consume the protected content.

To enable the enhanced licence chaining, a root encryption key is assigned to the policy. The root encryption key is used to cryptographically bind the leaf license to the root license. 

>[!NOTE]
>
>The enhanced license chaining is supported by Adobe Access clients version 3.0 and higher. If an older client requests a license for content that supports the enhanced license chaining, the license server can still issue a license to this client using license chaining supported by Adobe Access 2.0.

Example use case: Use this option to update any linked licenses by downloading a single root license. For example, implement subscription models where content can be played back as long as the user renews the subscription on a monthly basis. The benefit of this approach is that users only have to do a single license acquisition to update all of their subscription licenses.
