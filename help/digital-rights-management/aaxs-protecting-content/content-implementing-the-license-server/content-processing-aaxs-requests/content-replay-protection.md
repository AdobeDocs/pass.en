---
title: Replay protection
description: Replay protection
copied-description: yes
exl-id: dfb6d615-07d2-4303-82cc-10cfee4bb387
---
# Replay protection{#replay-protection}

For replay protection, it may be prudent to check whether the message identifier has been seen recently by calling `RequestMessageBase.getMessageId()`. If so, an attacker may be trying to replay the request, which should be denied. To detect replay attempts, the server can store a list of recently seen message ids and check each incoming request against the cached list. To limit the amount of time the message identifiers need to be stored, call `HandlerConfiguration.setTimestampTolerance()`. If this property is set, the SDK will deny any request that carries a timestamp more than the specified number of seconds off the server time.
