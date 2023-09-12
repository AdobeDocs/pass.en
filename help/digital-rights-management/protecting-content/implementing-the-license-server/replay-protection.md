---
title: Replay protection
description: Replay protection
copied-description: yes
---

# Replay protection{#replay-protection}

For replay protection, you may want to check whether the message identifier has been seen recently by calling `RequestMessageBase.getMessageId()`. If so, an attacker may be trying to replay the request, which should be denied. To detect replay attempts, the server can store a list of recently seen message ids and check each incoming request against the cached list. To limit the amount of time the message identifiers need to be stored, call `HandlerConfiguration.setTimestampTolerance()`. If this property is set, the SDK then denies any request that carries a timestamp for more than the specified number of seconds off the server time. 
