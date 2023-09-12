---
title: Pre-generating licenses
description: Pre-generating licenses
copied-description: yes
exl-id: d0bdd722-fd0e-4f34-87e7-28a564daf82b
---
# Pre-generating licenses{#pre-generating-licenses}

If you are pre-generating licenses that contain time-based usage rules, it is highly recommended that the license includes synchronization requirements (See *Using the Adobe Access SDK for Protecting Content* guide), so the license expiration can be enforced securely. Implementing a ‘heart beat' mechanism between the client and the server is highly recommended if you have any time-based restrictions in the license, since the heart beat will synchronize the client time with the server time.
