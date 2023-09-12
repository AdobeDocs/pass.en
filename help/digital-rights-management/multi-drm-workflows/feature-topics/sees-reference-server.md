---
description: One way to coordinate licensing and policy enforcement is to build these functions in to an entitlement server. Adobe provides the SEES reference entitlement server that you can work with to build your own server.
title: Reference Server  Sample ExpressPlay Entitlement Server (SEES)
exl-id: aa5b63f4-dffc-4808-8aa6-6b8f63df592c
---
# Reference Server: Sample ExpressPlay Entitlement Server (SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

One way to coordinate licensing and policy enforcement is to build these functions in to an entitlement server. Adobe provides the SEES reference entitlement server that you can work with to build your own server.

The reference server SEES demonstrates the ExpressPlay Entitlement Service, showing two services: basic time-based entitlement and device binding entitlement.

The SEES is built on top of two ExpressPlay Fairplay Services:

1. Expressplay Token Request Service
1. Expressplay Record Retrieving Service

The URL format for the ExpressPlay Token request takes two forms, one for production, one for the test environment:

**Production**: ht<span></span>tps://fp-gen.{prod_domain}/hms/fp/token

**Test**: ht<span></span>tps://fp-gen.test.expressplay.com/hms/fp/token

The URL format for ExpressPlay Record retrieving takes two forms, one for production, one for the test environment:

**Production**: ht<span></span>tps://api.{prod_domain}/cmiapi/getrecord/

**Test**: ht<span></span>tps://api.test.expressplay.com/cmiapi/getrecord/
