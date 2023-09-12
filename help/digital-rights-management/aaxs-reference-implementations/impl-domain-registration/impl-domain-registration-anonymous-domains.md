---
title: Anonymous Domains
description: Anonymous Domains
copied-description: yes
exl-id: a9358582-ad25-4016-94d2-cd82b4c00573
---
# Anonymous Domains {#anonymous-domains}

In this use case, a large number of devices belong to a single domain, and authentication may not be required. To use this type of domain with the reference implementation, create the policy specifying that the domain registration is required. Specify the domain server URL as `https:// host:port/flashaccess/domainserver/domainname/` and specify anonymous authentication.

The reference implementation implements the following logic for domain registration:

1. Parse the domain name from the request URL. 
1. Lookup the domain name in the `DomainServerInfo` table. If an entry is not found, insert an entry into the table (default values: authentication is not required and no membership maximum). 
1. If authentication is required for the requested domain, make sure a valid authentication token was included in the request, and match the Auth Namespace, if specified in the database.

    1. If authentication is required but no valid auth token was provided, return error `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Check if the device has already registered with the domain:

    1. Lookup the domain name in the `DomainMembership` table. For each machine GUID found, compare with the machine GUID in the request. If this is a new machine, add an entry to the `DomainMembership` table. 
    
    1. If it is a new device and Max Membership has already been reached, return error `DOM_LIMIT_REACHED (502)`.

1. Lookup all the domain keys for this domain in the `DomainKeys` table.

    1. If `DomainServerInfo` indicates the keys need to be rolled over, generate a new key pair, save it in the `DomainKeys` table (with key version one higher than the highest existing key), and reset the `Key Rollover Required` flag in `DomainServerInfo`. 
    
    1. For each domain key, generate a domain credential.

The reference implementation implements the following logic for domain de-registration:

1. Parse the domain name from the request URL. 
1. Lookup the requested domain name in the `DomainServerInfo` table. 
1. If authentication is required for the requested domain, make sure a valid authentication token was included in the request, and match the Auth Namespace, if specified in the database. 
1. Lookup the domain name and machine GUID in the `DomainMembership` table. If a matching entry is not found, return error `DEREG_DENIED (401)`. 

1. If this is not a preview request, delete the entry from `DomainMembership` and set the `Key Rollover Required` flag in `DomainServerInfo`.

In this use case, since a large number of machines could join the domain, completely matching the machine ID is not possible. Instead, the random machine GUID assigned to the machine during individualization is used.
