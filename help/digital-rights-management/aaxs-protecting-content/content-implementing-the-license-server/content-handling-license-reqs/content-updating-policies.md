---
title: Updating policies
description: Updating policies
copied-description: yes
exl-id: 0ea8d03b-68dd-415e-a75b-fd439bf858b6
---
# Updating policies {#updating-policies}

If policies are updated after the content is packaged, provide the updated policies to the license server so the updated version can be used when issuing a license. If your license server has access to a database for storing policies, you can retrieve the updated policy from the database and call `LicenseRequestMessage.setSelectedPolicy()` to provide the new version of the policy.

For license servers that do not rely on a central database, the SDK provides support for Policy Update Lists. A policy update list is a file containing a list of updated or revoked policies. When a policy is updated, generate a new Policy Update List and periodically push the list out to all the license servers. Pass the list to the SDK by setting `HandlerConfiguration.setPolicyUpdateList()`. If an update list is provided, the SDK consults this list when parsing the content metadata. `ContentInfo.getUpdatedPolicies()` contains the updated versions of policies specified in the metadata.

See [Working With Policies](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) and [Policy update lists.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
