---
title: Use machine identifiers
description: Use machine identifiers
copied-description: yes
---

# Use machine identifiers{#use-machine-identifiers}

All Adobe Primetime DRM requests (with the exception of requests supporting FMRMS compatibility) include information about the machine token that has been issued to the client during individualization. The machine token includes a Machine Id, which is an identifier that has ben assigned during individualization. You can use this identifier to count the number of machines from which a user has requested a license or joined a domain.

You can use an identifier as follows:

* The `getUniqueId()` method returns a string that has been assigned to a device during individualization. You can store the strings in a database and search by identifier. However, this identifier changes if the user reformats the hard drive and individualizes again. This identifier also has a different value between Adobe AIR and Adobe Flash Player in different browsers on the same machine. 
* If you want to more accurately count machines, you can use `getBytes()` to store the whole identifier. To determine if the machine has been seen before, get all the identifiers for a user name and call `matches()` to check if any match. Because the `matches()` method must be used to compare the values returned by `MachineId.getBytes`, this option is only practical when there are a small number of values to compare; for example, the machines associated with a particular user.

