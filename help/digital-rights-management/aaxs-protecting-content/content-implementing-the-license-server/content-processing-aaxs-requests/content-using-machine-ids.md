---
title: Using machine identifiers
description: Using machine identifiers
copied-description: yes
exl-id: 61ff9240-0c29-437e-b676-7983e2cc5f7b
---
# Using machine identifiers{#using-machine-identifiers}

All Adobe Access requests (with the exception of requests supporting FMRMS compatibility) contain information about the machine token issued to the client during individualization. The machine token contains a Machine Id, an identifier assigned during individualization. Use this identifier to count the number of machines from which a user has requested a license or joined a domain.

There are two ways of using the identifier. The `getUniqueId()` method returns a string assigned to the device during individualization. You can store the strings in a database and search by identifier. However, this identifier will change if the user reformats the hard drive and individualizes again. This identifier will also have a different value between Adobe® AIR® and Adobe® Flash® Player in different browsers on the same machine.

To more accurately count machines, you can use `getBytes()` to store the whole identifier. To determine if the machine has been seen before, get all the identifiers for a user name and call `matches()` to check if any match. Because the `matches()` method must be used to compare the values returned by `MachineId.getBytes`, this option is only practical when there are a small number of values to compare (for example, the machines associated with a particular user).
