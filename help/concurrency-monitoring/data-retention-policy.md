---
title: Data retention policy
description: Data retention policy
---

# Data retention policy {#data-retention-policy}

>[!WARNING]
>
>**Notice:** The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.


## Introduction {#introduction} 

Adobe, in its role as your data processor, must take appropriate measures to assist its customers in fulfilling access, deletion, and other requests from individuals. Applying appropriate, secure, and timely deletion policies is an important part of complying with this obligation. 

## Definitions {#definitions}

A Data Retention Policy determines how long Adobe stores customer's data. The default Data Retention Policy for Concurrency Monitoring is **25 months**. 

| Data Retention Period | The data retention period is the default data retention period (25 months). |
|---|---|
| **Data Retention Window** | The data retention window defines the parameters for which complete data can be viewed and reported. The data retention window is determined as follows:<br/> *Start date* = current date - data retention period <br/>*End date* = current date |

## Data collection {#data-collection} 

*Clickstream data* represents data shared by customers on the session heartbeats (for example, subjectID, mvpdName, and metadata). All custom metadata fields are referenced in the [Standard metadata attributes](/help/concurrency-monitoring/standard-metadata-attributes.md).

## Customer types {#customer-types}

### Current customers {#current-customers} 

Unless the customer purchases data retention extensions, Concurrency Monitoring will comply with the following customer data retention requirements:

* *Clickstream data* collected by Concurrency Monitoring must be deleted no later than **25 months** from the date of collection. 

### Terminated Customers {#terminated-customers}

A terminated customer is a customer who has ended the relationship with Adobe and is no longer using Concurrency Monitoring.

* *Clickstream data* collected by Concurrency Monitoring must be deleted within **6 months** from the customer's contract termination date.
 
## Data deletion {#data-deletion} 

Adobe retains the right to delete data for dates beyond the data retention period with no option for recovery. Data for current customers should be deleted on a rolling monthly basis.

