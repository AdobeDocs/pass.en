---
title: Sample Client Requests
description: Sample Client Requests
copied-description: yes
exl-id: 2b6a1349-aafc-4222-9081-525662f62961
---
# Sample Client Requests{#sample-client-requests}

You can collect a library of sample client requests using tools such as Charles Proxy or Wireshark. You should capture client requests after the Individualization server has been set up, using the Individualization Transport credential. You can then send these client requests (via *curl* or another tool) to the Individualization Server's end point to verify that the server is up and running properly. For example: 

```
curl https://<<yourindivserver:port>>/flashaccess/i15n/v5 -­data-binary  
@sample_client_request.bin > sample_client_response.ber
```

You may also want to send these requests again after any server configuration changes or ECI / CRL updates.

You should also update the Individualization Statistics page appropriately with successful individualization transactions.
