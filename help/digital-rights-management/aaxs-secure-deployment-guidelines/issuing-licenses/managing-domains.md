---
title: Managing Domains
description: Managing Domains
copied-description: yes
exl-id: c9030373-fd54-4745-9f03-0218532b9d6d
---
# Managing Domains{#managing-domains}

To prevent users from being able to backup and restore their files in an effort to bypass domain de-registration, it is recommended that one of the following approaches be implemented for domain management:

* Limit the amount of time the domain credentials are valid. Clients will need to contact the domain server to re-acquire domain credentials when they expire. At that time, the Domain Server can ensure that the machine is still authorized to be a member of the domain. 
* Rollover the domain keys each time a user de-registers. The License Server should only issue licenses to clients that have the latest domain key. This assumes that the License Server can co-ordinate with the Domain Server to know which key is the latest. Rolling over the domain keys involves generating a new key pair for the domain. When rolling over the keys for a particular domain, be sure to increment the key version in `generateDomainCredential`. For more information on implementing a key rollover, see *RefImplDomainReqHandler* in the Reference Implementation. 
* If the domain server is the same as the license server, the server can use the rollback counter to detect backup and restore. See *Processing Adobe Access requests *in *Using the Adobe Access SDK for Protecting Content.*
