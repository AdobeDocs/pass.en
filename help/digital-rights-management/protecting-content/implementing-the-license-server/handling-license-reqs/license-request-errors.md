---
title: License request error handling
description: License request error handling
copied-description: yes
exl-id: 7cfdebc5-db2b-4629-98e6-31ad71cb424c
---
# License request error handling {#license-request-error-handling}

If an error occurs during request parsing, a `HandlerParsingException` occurs. This exception includes error information that is returned to the client. If you need to retrieve the error information, you need to call `HandlerParsingException.getErrorData()`. If an error occurs during the generation of a license because of DRM policy requirements that have not been satisfied, a `PolicyEvaluationException` occurs. This exception also includes `ErrorData` to be returned to the client.

See the API documentation for `LicenseRequestMessage.generateLicense()` for details on how DRM policies are evaluated during license generation.
