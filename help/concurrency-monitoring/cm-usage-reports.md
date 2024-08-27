---
title: Concurrency Monitoring Usage Reports
description: Concurrency Monitoring Usage Reports
exl-id: 20220436-e748-4b22-8e7c-e074e0bfe242
---
# Concurrency Monitoring Usage Reports {#cm-usage-reports}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.



## Overview {#usage-rep-overview}

The **Concurrency Monitoring Usage Reports** service is available via a REST API which provides insight into the concurrent usage as reported by the customer's applications.

## Prerequisites {#usage-rep-prerequisites}

In order to access the Concurrency Monitoring Usage Reports product, a customer must first contact the Concurrency Monitoring [Support Team](mailto:tve-support@adobe.com) and they will carry out the necessary steps to allow you access to the API product. More details on [CMU API Access](/help/concurrency-monitoring/cmu-api-access.md). 

## General Report Metrics & Breakdowns {#general-rep-metrics-breakdown}

### Usage Reports users can monitor the following metrics:{#monitor-metrics}

| Name | Description |
|:---|:---|
| active-users       | number of distinct user accounts that have initiated at least one streaming session during the interval, broken down by time granularity                                                  |
| active-sessions    | number of streaming sessions that have reported activity during the interval (it does not include failed attempts, sessions that received a deny response for the initialization call)    |
| started-sessions   | number of streaming sessions that were started within the interval                                                                                                                        |
| completed-sessions | number of streaming sessions that were finished during the interval (either explicitly or due to timeout)                                                                                 |
| failed-attempts    | number of session initialization attempts that received a deny response                                                                                                                   |
| dismissed-sessions | number of streaming sessions that were finished during playback (on heartbeat) due to a policy violation. This metric is meaningful only where a FIFO or last_one_wins policy is enacted. |
| killed-sessions    | number of streaming sessions that were explicitly killed upon starting a new session (via X-Terminate header)                                                                             |
| duration_0-15      | number of streams with a duration between 0 and 15 minutes                                                                                                                                |
| duration_15-30     | number of streams with a duration between 15 and 30 minutes                                                                                                                               |
| duration_30-60     | number of streams with a duration between 30 and 60 minutes                                                                                                                               |
| duration_60-120    | number of streams with a duration between 60 and 120 minutes                                                                                                                              |
| duration_2h-4h     | number of streams with a duration between 2 hours (120 minutes) and 4 hours                                                                                                               |
| duration_4h-8h     | number of streams with a duration between 4 hours and 8 hours                                                                                                                             |
| duration_8h-16h    | number of streams with a duration between 8 hours and 16 hours                                                                                                                            |
| duration_16h-1d    | number of streams with a duration between 16 hours and 1 day (24 hours)                                                                                                                   |
| duration_1d-3d     | number of streams with a duration between 1 day and 3 days                                                                                                                                |
| duration_3d-7d     | number of streams with a duration between 3 days and 7 days                                                                                                                               |
| duration_1w-1m     | number of streams with a duration between 1 week (7 days) and 1 month (30 days)                                                                                                           |
| duration_over-1m   | number of streams with a duration over 1 month (30 days)                                                                                                                                  |

### Usage Reports users can filter the metrics listed above by the following dimensions: {#dimensions-2-filter-metrics}

| Dimension Name | Description                                                                                                       |
|:---------------|:------------------------------------------------------------------------------------------------------------------|
| year           | The 4 digit year                                                                                                  |
| month          | The month of the year (1-12)                                                                                      |
| day            | The day of the month (1-31)                                                                                       |
| hour           | The hour of the day                                                                                               |
| minute         | The minute of the hour[^1]                                                                                        |
| application    | The application name registered in Concurrency Monitoring used to manage sessions                                 |
| application-id | The application ID registered in Concurrency Monitoring used to manage sessions                                   |
| channel        | The channel metadata sent during the initialization of the session (marked as Unknown if no metadata is sent)     |
| mvpd           | The MVPD provided at session management                                                                           |
| platform       | The platform metadata provided at session initialization or pre-defined for an application at configuration level |

## Concurrency Report Metrics & Breakdowns {#concurrency-reports-metrics-breakdown}

Starting with Concurrency Monitoring version 2.9.0 we have introduced a new report for understanding concurrent usage: a histogram for **concurrency-level** and **activity-level**. 

The main purpose of this report is to help you understand the impact of setting a policy with certain concurrency limit and to give you enough information to decide if you should raise the limit.

### Usage Reports users can monitor the following metrics: {#metrics-usage-rep-users}

|  Dimension Name |                            Description                           |
|:---|:---|
| users           | number of users who have reached each concurrency/activity level |

### Usage Reports users can filter the metrics listed above by the following dimensions: {#dimensions-to-filter-metrics}

| Dimension Name  | Description |
|:---|:---|
| year              | The 4 digit year                                                                                                                                                                                                                                                                  |
| month             | The month of the year (1-12)                                                                                                                                                                                                                                                      |
| day               | The day of the month (1-31)                                                                                                                                                                                                                                                       |
| concurrency-level | Represents any distinct **stream activity that was approved at the session initialization phase** for a user in order to be able to observe how many concurrent streams **were opened** by a user and to understand the impact of applying a certain concurrency limit                    |
| activity-level    | Represents any distinct **stream activity (no matter of its state: started, active, stopped, rejected)** for a user in order to be able to observe how many concurrent streams were tried to be opened by a user and to understand the impact of applying a certain concurrency limit |
| mvpd              | The MVPD provided at session management                                                                                                                                                                                                                                           |

### Reports examples
For best data accuracy, we recommend the reports presented on this page [CMU reports examples](/help/concurrency-monitoring/cm-usage-reports-examples.md)

[^1]: Minutely reports are not available by default. Please contact the Concurrency Monitoring [Support Team](mailto:tve-support@adobe.com) to request them. 