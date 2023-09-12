---
title: Anonymous domain logic
description: Anonymous domain logic
copied-description: yes
exl-id: 4a6c3485-cde7-403f-89d8-f6420df3539a
---
# Anonymous domain logic{#anonymous-domain-logic}

## Domain registration logic {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

The reference implementation applies the following logic for anonymous domain registration:

1. Parse the domain name from the request URL. 
1. Look up the domain name in the `DomainServerInfo` table. 
1. If you cannot locate an entry, insert an entry in the table.

   The default values are:

    * `authentication is not required`
    * `no membership maximum`

   If authentication is required for the requested domain, ensure that a valid authentication token is in the request. If the Auth Namespace is specified in the database, the token must match the specified Auth Namespace. 
1. If authentication is required, but a valid auth token is not available, return error `DOM_AUTHENTICATION_REQUIRED (503)`. 
1. Check whether the device is registered with the domain:

    1. Look up the domain name in the `DomainMembership` table. 
    1. Compare the machine GUID that you locate with the machine GUID in the request. 
    1. If this is a new machine, add an entry in the `DomainMembership` table. 
    1. If it is a new device and `Max Membership` value has been reached, return error `DOM_LIMIT_REACHED (502)`.

1. Look up all the domain keys for this domain in the `DomainKeys` table:

    1. If `DomainServerInfo` indicates that the keys need to be rolled over, generate a new key pair. 
    1. Save the keypair in the `DomainKeys` table, with a key version that is one number higher than the highest existing key. 
    1. Reset the `Key Rollover Required` flag in `DomainServerInfo`. 
    
    1. For each domain key, generate a domain credential.

## Domain de-registration logic {#section_C968BBFCBFAB4510A903D169F38C9FCE}

The reference implementation applies the following logic for anonymous domain de-registration:

1. Parse the domain name from the request URL. 
1. Look up the requested domain name in the `DomainServerInfo` table. 
1. If authentication is required for the requested domain, ensure a valid authentication token is in the request.

   The token must also match the Auth Namespace that is specified in the database. 
1. Look up the domain name and machine GUID in the `DomainMembership` table.

   If you cannot locate a matching entry, return error `DEREG_DENIED (401)`. 

1. If this is not a preview request, delete the entry from `DomainMembership`, and in `DomainServerInfo`, set the `Key Rollover Required` flag.

Because a large number of machines may join the domain, you cannot simply match the machine ID. Instead, the random machine GUID that is assigned to the machine during individualization is applied.
