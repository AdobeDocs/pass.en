---
title: Overview
description: Overview
copied-description: yes
exl-id: 15733120-b1bb-46a7-90d2-4eb11c539d62
---
# Overview  {#overview}

Using Adobe® Access™, content providers can apply policies to media files. Using the policy management APIs, administrators can create, view details of, and update policies.

A *policy* defines how users can view content; it is a collection of information that includes security settings, authentication requirements, and usage rights. When policies are applied, encryption and signing allow content providers to maintain control of their content no matter how widely it is distributed. Protected files can be delivered by using Adobe® Flash® Media Server or an HTTP server. They can be downloaded and played in custom players built with Adobe® AIR®, Adobe® Flash® Player, and Adobe® Primetime SDK for iOS. The policy is a template for the license server to use when it generates a license. The client may also refer to the policy before requesting a license to determine whether it needs to prompt the user to authenticate before issuing a license request to the server.

A policy specifies one or more rights that are granted to the client. Typically, a policy includes, at a minimum, the "Play Right". It is also possible to specify multiple Play Rights, each with different restrictions. When the client encounters a license with multiple Play Rights, it uses the first one for which it meets all the restrictions. For example, this feature can be used to enforce different output protection settings on different platforms. For sample code illustrating this example, see `CreatePolicyWithOutputProtection.java` in the Reference Implementation Command Line Tools "samples" directory.

You can accomplish the following tasks by using the policy management APIs:

* Create and update policies 
* View policy details 
* Manage policy update lists

For details about the Java API discussed in this chapter, see *Adobe Access API Reference*.

For information about the Policy Manager reference implementation, see *Using the Adobe Access Reference Implementations*.
