---
title: FAQ
description: FAQ
copied-description: yes
exl-id: 9058604e-dbab-4df5-89fd-1219c85c7643
---
# FAQ {#faq}

* How often do ECI changes occur? 
  * Anytime a new Adobe DRM client is released, an ECI device record is added. 

* How large are ECI files?
  * They are typically less than 1 Kilobyte per device record.

* What happens if the server is missing an ECI device record? 
  * That particular class of clients will not be able to individualize against the On Premises Individualization Server and errors will be logged to the log files. 

* What happens if a server's CRLs are expired? 
  * The server will stop functioning correctly and errors will be logged to the log files.
