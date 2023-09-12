---
title: Revoking client credentials
description: Revoking client credentials
copied-description: yes
exl-id: 583dff28-c34a-4759-81a6-0471feab309f
---
# Revoking client credentials{#revoking-client-credentials}

Under certain conditions it is necessary to revoke a client's credentials or check whether a given set of credentials have already been revoked. Credentials may be revoked if the credentials are compromised. When this happens, licenses will no longer be issued to compromised clients.

Adobe maintains Certificate Revocation Lists (CRLs) for revoking compromised clients. These CRLs are automatically enforced by the SDK. License servers may further restrict clients by disallowing particular machine credentials or particular versions of DRM and runtime credentials. A `RevocationList` may be created and passed into the SDK to revoke machine credentials. Particular DRM/runtime versions can be revoked either at the policy level (by setting module restrictions in the play right) or globally (by setting module restrictions in the `HandlerConfiguration`).

The discussion in this chapter will be centered on revoking client credentials.
