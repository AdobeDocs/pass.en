---
title: Troubleshoot and debug
description: Troubleshoot and debug
copied-description: yes
exl-id: 1fcacd29-627d-4536-a746-16ddcfc8bc34
---
# Troubleshoot and debug {#troubleshooting-debugging}

Primetime Ad Insertion offers tools to identify and diagnose issues that can occur in all phases of video delivery, such as CDN delivery errors, ad creative errors or client connectivity errors.

Primetime Ad Insertion supports verbose logging via the [Bootstrap API parameter](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` or `ptdebug=AdCall` to the bootstrap URL. Logs are output to both HTTP response headers and to the Primetime Ad Insertion console. This parameter is meant for localized testing only, not for production streams. For more information on message types when verbose logging is enabled, see [ptdebug logging events in verbose logging](verbose-logging.md#ptdebug-logging-events).

Primetime Ad Insertion also provides performance debugging on all requests with the X-ADBE-AI-X1 header, which can be used to measure performance and ad insertions on any given request. This request header is available regardless of whether verbose logging is enabled. For more information, see [Verbose headers: X-ADBE-PTAI-X1](debugging-headers.md).
