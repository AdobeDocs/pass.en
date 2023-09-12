---
title: Revoking DRM client and runtime credentials
description: Revoking DRM client and runtime credentials
copied-description: yes
exl-id: 3a91a256-ab01-48d8-99f3-854195faae6f
---
# Revoking DRM client and runtime credentials {#revoking-drm-client-and-runtime-credentials}

DRM/Runtime versions are identified by security level, version number, and other attributes including Operating System and runtime. To restrict the DRM/Runtime versions allowed, set the module restrictions in a DRM policy or in a `HandlerConfiguration`. Module restrictions may include a minimum security level and list of module versions that are not permitted to be issued a license.

See [Block list of DRM Clients restricted from accessing protected content](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) for details on the attributes used to identify a DRM/Runtime module.

If the minimum security level is set, the version on the client (specified in the machine token), must be greater than or equal to the specified value.

If a list of excluded versions is specified and the client's version matches any of the version identifiers in the list, the client will not be allowed to use a right containing this ModuleRequirements instance. For a module to match the version information, all parameters specified in the version information, except for the release version, must exactly match the modules's values. The release version matches if the client module's value is less than or equal to the value in the version information.

In the event a breach is reported with a particular DRM client or runtime version, the content owner and content distributer (who runs the license server) can configure the server to refuse to issue licenses during a period in which Adobe does not have a fix available. This can be configured through the `HandlerConfiguration` as described above, or by making changes to all the DRM policies. In the latter case, you can maintain a DRM policy update list and use it to check whether a DRM policy has been updated or revoked.

If you require a newer version of the Adobe Flash Player/Adobe AIR Runtime or the Adobe Content Protection library (DRM module), you need to update your DRM policies.

See [Updating a policy using the Java API](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

Then you need to create a DRM Policy Update List or set restrictions in `HandlerConfiguration` by invoking `HandlerConfiguration.setRuntimeModuleRequirements()` or `HandlerConfiguration.setDRMModuleRequirements()`. When a user requests a new license with the specified block lists enabled, you need to install the latest runtimes and libraries before a license can be issued.

See the sample code in [Updating a policy using the Java API For an example on block listing DRM and runtime versions](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) for an example on block listing DRM and runtime versions.
