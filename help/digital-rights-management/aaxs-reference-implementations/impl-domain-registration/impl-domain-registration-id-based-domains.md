---
title: Identity-based domains
description: Identity-based domains
copied-description: yes
exl-id: de7b6c8a-5227-4679-933a-3278921903d7
---
# Identity-based domains {#identity-based-domains}

In this use case, each authenticated user has his own domain, and a certain number of devices are allowed to join the domain. To use this type of domain with the reference implementation, create a policy specifying domain registration is required. Specify your server's host and port for the domain server URL and specify username/password authentication is required.

The reference implementation implements the following logic for domain registration:

1. Determine the domain name to assign to this user. The domain name will be * `namequalifier:username`* extracted from the authentication token. If there is no authentication token, return error DOM_AUTHENTICATION_REQUIRED (503). 
1. Lookup the domain name in the `DomainServerInfo` table. If an entry is not found, insert an entry into the table (default values are authentication required, max domain membership=5). 
1. Check if the device has already registered with the domain:

    1. Lookup the domainname in the `UserDomainMembership` table. For each machine ID found, compare with the machine ID in the request. If this is a new machine, add an entry to the `UserDomainMembership` table. Next, find the matching records in `UserDomainRefCount` table. If an entry does not exist for this machine GUID, add a record. 
    
    1. If it is a new device and Max Membership has already been reached, return error DOM_LIMIT_REACHED (502).

1. Lookup all the domain keys for this domain in the DomainKeys table.

    1. If `DomainServerInfo` indicates that the keys need to be rolled over, generate a new key pair, save it in the `DomainKeys` table (with key version one higher than the highest existing key), and reset the “Key Rollover Required” flag in `DomainServerInfo`. 
    
    1. For each domain key, generate a domain credential.

The reference implementation, implements the following logic for domain de-registration:

1. Determine the domain name to assign to this user. The domain name will be *namequalifier:username* extracted from the authentication token. If there is no authentication token, return error DOM_AUTHENTICATION_REQUIRED (503). 
1. Lookup the requested domain name in the `DomainServerInfo` table. 
1. Lookup the domain name in the `UserDomainMembership` table. For each machine ID found, compare with the machine ID in the request. Find the corresponding entry in the `UserDomainRefCount` table. If a matching entry is not found, return error DEREG_DENIED (401). 

1. If this is not a preview request, delete the entry from `UserDomainRefCount` table. If there are no more entries in that table for the machine, delete the entry from `UserDomainMembership` and set the “Key Rollover Required” flag in `DomainServerInfo`.

In this use case, each user is allowed to register a small number of machines, so we can use the full machine ID and the `matches()` method to accurately count machines. However, since the user could register multiple times on this machine (through multiple AIR applications or Players in different browsers), the server also needs to maintain a reference count, so that the de-registration can be counted accurately. The de-registration cannot be considered complete, until all the domain tokens on the machine are surrendered.
