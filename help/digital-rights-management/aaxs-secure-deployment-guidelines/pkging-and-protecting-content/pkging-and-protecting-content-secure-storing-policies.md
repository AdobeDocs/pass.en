---
title: Securely storing policies
description: Securely storing policies
copied-description: yes
exl-id: fd335a0c-7eb1-4159-958f-7302fce98cef
---
# Securely storing policies{#securely-storing-policies}

Adobe Access SDK provides a great deal of flexibility in the development of applications for use in content packaging and policy creation. When creating such applications, you may want to allow some users to create and modify policies, and limit other users such that they can only apply existing policies to content. If this is the case, you must implement the necessary access controls to create user accounts with different privileges for policy creation and the application of policies to content.

Policies are not signed or otherwise protected from modification until they are used in packaging. If you are concerned about users of your packaging tools modifying policies, you should consider signing the policies to ensure that they cannot be modified.

For more information on creating applications using the SDK, see the *Adobe Access API Reference*.
