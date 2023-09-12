---
title: BEES Error codes
description: BEES Error codes
copied-description: yes
exl-id: 36c83ee9-7e28-442e-8076-691a1bd43a01
---
# BEES Error codes {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

If there is an error during a BEES check, a `DRMErrorEvent` will be returned to the client. You can parse this event's properties to find details on the nature of the failure. A subset of possible error codes are listed below. 

|  Error  | Description  |
|---|---|
| `3304:305`  |Generic Authorization error from  Primetime Cloud DRM attempting to handle an authentication / authorization request. Typically not associated with a BEES issue. If this error is consistently encountered, you should submit a trouble ticket to the  Primetime Cloud DRM team along with diagnostic information.  |
| `3329:0`  | Application Specific Error (from the BEES Authorizer). If no sub-error code was returned, the error text will display details of the issue. For instance, there was an issue parsing the response, or the BEES server was unreachable.  |
| `3329:<HTTP error code>`  | An HTTP response other than 200 was issued by the BEES server. The HTTP error code is returned to the client in the suberror code field. This could indicate a configuration problem, or a BEES server outage.  |
| `3329:<x>`  |BEES server DISALLOWED the license request. The sub-error code and error text are specified by the BEES server within the JSON response's `error` and `errorText` properties. This kind of response should not be considered an error, but rather a regular denial response from your BEES server.  |
