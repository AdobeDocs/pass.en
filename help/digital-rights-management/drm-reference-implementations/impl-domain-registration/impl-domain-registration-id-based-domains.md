---
title: Identity-based domain registration logic
description: Identity-based domain registration logic
copied-description: yes
exl-id: 6e391fce-00b4-45cf-b785-3b0ec734a11e
---
# Identity-based domain registration logic{#identity-based-domain-registration-logic}

## Domain registration logic {#section_149C247458954877AF158B4A09A8526B}

The reference implementation applies the following logic for identity-based domain registration:

1. Determine the domain name to assign to a designated user.

   The domain name ( `namequalifier:username`) is extracted from the authentication token. If a token is not available, error  is thrown. 
1. Look up the domain name in the `DomainServerInfo` table.

   If no entry is found, insert an entry. The default values are:

    * `authentication required` 
    * `max domain membership=5`

   . 

1. To verify that the device has been registered with the domain:

    1. Look up the `domainname` in the `UserDomainMembership` table:

        1. For each machine ID that is located, compare the ID with the machine ID in the request. 
        1. If this is a new machine, add an entry to the `UserDomainMembership` table. 
        1. Search for the matching records in `UserDomainRefCount` table. 
        1. If an entry does not exist for this machine GUID, add a record.

    1. If it is a new device, and the `Max Membership` value has been reached, return error .

1. Look up all the domain keys for this domain in the `DomainKeys` table:

    1. If `DomainServerInfo` indicates that the keys need to be rolled over, generate a new key pair, 
    1. Save the pair in the `DomainKeys` table, with a key version that is one higher than the highest existing key. 
    1. Reset the `Key Rollover Required` flag in `DomainServerInfo`. 
    
    1. For each domain key, generate a domain credential.

## Domain de-registration logic {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

The reference implementation applies the following logic for identity-based domain de-registration:

1. Determine the domain name to assign to this user.

   The domain name is `namequalifier:username`, which is extracted from the authentication token. If no token is available, return error `DOM_AUTHENTICATION_REQUIRED (503)` occurs. 
1. Look up the requested domain name in the `DomainServerInfo` table. 
1. Look up the domain name in the `UserDomainMembership` table. 
1. Compare each machine ID that you find with the machine ID in the request. 
1. Locate the corresponding entry in the `UserDomainRefCount` table.

   If a matching entry is not located, return error . 

1. If this is not a preview request, delete the entry from the `UserDomainRefCount` table. 
1. If there are no additional entries in that table for the machine, delete the entry from `UserDomainMembership` and set the [!DNL Key Rollover Required] flag in the `DomainServerInfo` property.

Each user can register a small number of machines, so you can use the full machine ID and the `matches()` method to count machines. Because a user can register multiple times, through multiple AIR applications or Players in different browsers, the server needs to maintain a reference count so that de-registration can also be counted.

>[!NOTE]
>
>De-registration is not complete until all of the domain tokens on the machine are surrendered.
