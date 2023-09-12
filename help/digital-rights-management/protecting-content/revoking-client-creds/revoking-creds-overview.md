---
title: Overview
description: Overview
copied-description: yes
exl-id: 332343ce-ac22-41a5-801a-3597476f0eaf
---
# Overview{#overview}

You may need to revoke a client's credentials or check whether a given set of credentials have already been revoked under certain conditions. Credentials may be revoked if they are compromised. When these issues occur, licenses are no longer issued to compromised clients.

Adobe maintains Certificate Revocation Lists (CRLs) for revoking compromised clients. These CRLs are automatically enforced by the SDK. License servers may further restrict clients by disallowing particular machine credentials or particular versions of DRM and runtime credentials. A `RevocationList` may be created and passed into the SDK to revoke machine credentials. Particular DRM/runtime versions can be revoked either at the DRM policy level by setting module restrictions in the play right or globally by setting module restrictions in the `HandlerConfiguration`.

The discussion is centered on revoking client credentials.
