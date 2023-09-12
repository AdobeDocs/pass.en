---
title: Updating DRM policies
description: Updating DRM policies
copied-description: yes
exl-id: 27dc35d2-134c-4b88-9251-c6bb04a48f13
---
# Updating DRM policies {#updating-drm-policies}

If DRM policies are updated after the content is packaged, provide the updated DRM policies to the license server so the updated version can be used when issuing a license. If a license server has access to a database for storing DRM policies, you can retrieve the updated DRM policy from the database and call `LicenseRequestMessage.setSelectedPolicy()` to provide the new version of the DRM policy.

For license servers that do not rely on a central database, the SDK provides support for DRM Policy Update Lists. A DRM policy update list is a file that includes a list of updated or revoked DRM policies. When a DRM policy is updated, generate a new DRM Policy Update List and periodically push the list to all license servers. Pass the list to the SDK by setting `HandlerConfiguration.setPolicyUpdateList()`. If an update list is provided, the SDK consults this list when it parses the content metadata. `ContentInfo.getUpdatedPolicies()` includes the updated versions of DRM policies specified in the metadata.

See [Working With DRM Policies](../../../protecting-content/working-policies-overview/working-with-policies.md) and [DRM policy update lists](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
