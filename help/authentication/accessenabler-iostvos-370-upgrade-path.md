---
title: AccessEnabler iOS/tvOS 3.7.0 Upgrade Path
description: AccessEnabler iOS/tvOS 3.7.0 Upgrade Path
exl-id: f15c7414-ec9b-4e21-b457-1ecf59f47441
---
# AccessEnabler iOS/tvOS 3.7.0 Upgrade Path {#accessenabler-iostvos-370-upgrade-path}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

Keychain storage changes from the [new AccessEnabler version 3.7.0](/help/authentication/authn-rn-ios-tvos-370.md) are incompatible with Keychain storage implementation from AccessEnabler version's lower than 3.7.0.

The upgrade path for one application adopting the new AccessEnabler version 3.7.0 will migrate all tokens from previous version/s of Keychain storage. Therefore, end users **should not experience loss of authentication / authorization sessions** during the AccessEnabler framework update process.

## Known Limitations

Some limitations, described below, might be encountered by implementers.


1. Regular (Adobe) SSO will not work between one application using AccessEnabler version 3.7.0 and one application using AccessEnabler version/s lower than 3.7.0, even for applications developed by the same vendor.

    >[!IMPORTANT]
    >
    >* System level (Apple) SSO will not be affected! 
    >
    >* Regular (Adobe) SSO will continue to work if both applications are developed by the same vendor and use AccessEnabler version/s lower than 3.7.0! 
    >
    >* Regular (Adobe) SSO will work if both applications are developed by the same vendor and use AccessEnabler version 3.7.0!


1. In the situation of downgrading one application using AccessEnabler version 3.7.0 to a lower version of AccessEnabler, then new generated tokens will not be migrated. Therefore, end users might experience the loss of authentication / authorization sessions, without expecting it.

    >[!IMPORTANT]
    >
    >* End users authenticated through system level (Apple) SSO will not be affected!
    >* End users which were already authenticated before updating to the new application using AccessEnabler version 3.7.0 will not be affected!

1. In the situation of downgrading one application using AccessEnabler version 3.7.0 to a lower version of AccessEnabler, then deleted tokens will not be acknowledged. Therefore, end users might experience the presence of authentication / authorization sessions, without expecting it.
