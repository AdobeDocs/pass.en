---
title: Account IQ glossary
description: A glossary of product terminologies.
exl-id: 2ee54442-9538-4c30-b999-265310b3935f
---
# Product concepts and glossary {#glossary}

The following product terminologies and their definitions are common to all versions of Account IQ.

## [!UICONTROL Accounts Sharing Probability] {#account-sharing-probability-def}

A dashboard panel with charts that divides the current segments sharing scores into sharing range categories of Very Low, Low, Moderate, High, and Very High.

## [!UICONTROL Action] {#action-def}

A direct or indirect event associated with an [Operation](#operation-def) that affects the characteristics (for example, Sharing score or number of devices in use) of a related operation segment (or cohort).

## [!UICONTROL Aggregated sharing score] {#sharing-probability-level-def}

A dashboard panel with charts that divides the current segments sharing scores into sharing range categories of Very Low, Low, Moderate, High, and Very High, along with each categories percentage of the total amount of streaming for the segment.

## [!UICONTROL AuthN] {#authn-def}

The number of authentication attempts. An authentication attempt is the process whereby a user attempts to login with D2C service or MVPD. For TV Everywhere users, the user is redirected to their chosen MVPD, where they identify themselves to the MVPD - typically with a username and password.

## [!UICONTROL AuthN OK] {#authn-ok-def}

The number of successful authentications. A successful authentication occurs when a users identify is confirmed by a D2C service or MVPD. For TV Everywhere users, this results in the user being redirected back to the programmer app or site.

## [!UICONTROL Cluster] {#cluster-def}

A cluster is a collection of locations and devices. The clusters are created by finding common locations between devices. The devices that have been seen in a common location will be considered to belong in the same cluster. Two devices can be in the same cluster even though they do not have common locations but can be connected through the locations of other devices.

### [!UICONTROL Mobile cluster] {#mobile-cluster-def}

A cluster that has no static devices.

### [!UICONTROL Static cluster] {#static-cluster-def}

A cluster that has at least one static device.

## [!UICONTROL Concurrency] {#consurrency-def}

The concurrent is defined by two (or more) streams played at the same time or very close in time so that the interval between them cannot be justified by traveling at a normal speed.
Concurrent usage is calculated using the maximum speed(miles/hour) between 2 different clusters. A user is considered to have concurrent usage if he has a speed greater than 124 m/h on a distance lesser than 124 miles or if he has a speed greater than 400 m/h on a distance greater than 124 miles. The distance is calculated between locations from different clusters. Concurrent usage is allowed in the same cluster.

## [!UICONTROL Device] {#device-def}

A digital video hardware product capable of playing upstreaming content. For example, smart phones, laptop and desktop computers, game consoles, and smart televisions.

## [!UICONTROL Evaluation period] {#evaluation-period-def}

Evaluation period is the time from the beginning of the action associated with Operation until the  end of the action or it's measurement.

## [!UICONTROL Geographical Span] {#geographical-span-def}

The distance between the farthest points in a set of locations.

## [!UICONTROL Granularity] {#granularity-def}

In reference to time interval, the size of the period; such as one week or one month.

## [!UICONTROL IP] {#ip-def}

The Internet Protocol address assigned to a device by an Internet Service Provider. For example, cable service provider, and cell service provider.

## [!UICONTROL Location] {#location-def}

A unique point on earth. It is also refered to as the geolocation for a specific play request with a precision of 1000m x 1000m (one square km).

## [!UICONTROL Media Company] {#media-company-def}

Media Company is a company that owns a group of media networks.

## [!UICONTROL Metric] {#metric}

Metric is an attribute of subscriber account (for example, their MVPD, the programmers and channels of the content they stream, the number of devices they use).

## [!UICONTROL Mobile device] {#mobile-device-def}

A device that has high mobility. For example, mobile phone, and tablet.

## Operation {#operation-def}

Operation is a record created to track the effect of a particular [action](#action-def) on an associated segment. An example of an action can be a limit placed on the number of concurrent streams allowed for accounts identified by the segment.

## [!UICONTROL Overall sharing score] {#overall-sharing-score}

A value that helps users understand the magnitude of password sharing and provide them a sense of urgency to act upon it.

## [!UICONTROL Play Request] {#play-requests-def}

Equivalent to a stream start. This event marks the beginning of a user streaming content.

## [!UICONTROL Risk Index - Usage] {#risk-index-usage}

Also known as Usage from Shared Accounts, it is a value calculated based on the number of play requests made by the each account weighted by each account's sharing probability. It is also known as Usage by Shared Accounts Risk Index.

## [!UICONTROL Segment] {#segmet-def}

Segment is a set of accounts that meet the user defined conditions specified by the selected metrics. For example, "users in region A, B, C, D or E that have more than three devices".

## [!UICONTROL Sharing level] {#sharing-level-def}

Also known as Risk Index - Accounts or Shared Accounts Risk Index, it is a value calculated based on an average of the sharing probability computed for every account in the current segment that has streamed at least once during the selected time interval.

## [!UICONTROL Static device] {#static-device-def}

A device that has very low mobility. For example, game console, set top box, and television set.

## [!UICONTROL Time interval] {#time-interval-def}

Also known as period, it is the window of time that contains the play request activity represented in the user interface and tables from start to finish.

## [!UICONTROL Trend] {#trend-def}

The percentage difference in the associated metric (for example, percentage of total play requests) between the current and previous period.

## [!UICONTROL Unique Subscribers] {#unique-subscriber-def}

The number of unique accounts that have streamed at least once during a given period. 

## [!UICONTROL Usage] {#usage-defs}

### [!UICONTROL Avid user] {#avid-user-def}

More than 37 play request per month.

### [!UICONTROL Infrequent user] {#infrequent-users-def}

Less than 9 play requests per month.

### [!UICONTROL Regular user] {#regular-user-def}

From 9 to 37 play requests per month.

## [!UICONTROL Usage Pattern] {#usage-patern-def}

One of a finite set of category labels applied to an account that best characterizes the users of the account in terms of social groups or behaviors (e.g., a small family, a traveler or commuter, social sharing, etc.).

## [!UICONTROL Video category] {#video-category-def}

### [!UICONTROL For D2C service] {#d2c-service}

A video category is a specific label that qualifies the nature of the video. For example, region of the source, content types, such as VOD or live, event, or specific labels such as team.

### [!UICONTROL For TV Everywhere] {#tv-everywhere}

A video category is defined by the combination of Programmer, channel, and MVPD associated with the stream.

## [!UICONTROL Zip Code] {#zip-code-def}

The U.S. Postal code associated with locations within the U.S.
<!--calculated metrics-->

</br>


## TV Everywhere specific terminology

### [!UICONTROL AuthZ] {#authz-def}

Authorization, or the number of authorization request. An authorization request is the process whereby a programmer requests permission from an MVPD through Adobe to begin streaming a user's requested content. The MVPD typically grants the request based on the content rights associated with the user's MVPD subscription (for example whether the channel associated with the content is in the user's subscription). Some authorization request responses are cached by Adobe, which allows Adobe to respond immediately without passing the request on to the MVPD.

### [!UICONTROL AuthZ OK] {#authz-ok-def}

The number of successful authorizations.

### [!UICONTROL Channel] {#channel-def}

Channel, also knows as Property, is a thematically related source of video content. Traditionally representing a distinct, numerically addressable continuous video feed from an MVPD. The channel directly maps to an accessible channel of content available to the subscribers through their Set Top Box (STB).

### [!UICONTROL Industry Average Index] {#industry-avg-index-def}

A value computed for each of the Risk Indices (Accounts, Usage, Overall) across all Programmers and MVPDs during the selected time interval.

### [!UICONTROL Isolation Mode] {#isolation-mode-def}

A type of sharing analysis where the evaluation of an account is limited to events that occurred directly on the programmers in the selected segment.  Normally, all account events are evaluated, which provides a much more accurate estimate of sharing.  Some MVPD data is structured in a way that only allows for Isolation Mode analysis.

### [!UICONTROL MVPD] {#mvpd-def}

MVPD, also known as Distributor, is aggregator, reseller, and distributor of Media Company video content.

### [!UICONTROL Programmer] {#programmer-def}

Programmer, also known as Network, is a company that is subsidiary of a larger company (corporation) that owns and manages one or more channels.

### [!UICONTROL requestorID] {#requestorid-def}

The ID a Media Company Uses to identify themselves or a subsidiary to an MVPD.  Depending on Programmer implementation, this could map to a Media Company, Programmer or Channel.  The most common The ID a Media Company Uses to identify themselves or a subsidiary to an MVPD.  Depending on Programmer implementation, this could map to a Media Company, Programmer or Channel.  Traditionally, this mapped to a Channel.  With the creation of pseudo-Channels like MML (March Madness Live) and technically driven moves to address MVPD-driven data limitations, requestorID is beginning to become more associated with the Media Company.

### [!UICONTROL resourceID] {#resource-id-def}

The content requested by the end user. Traditionally, this has identified the Channel associate with the content the user has requested.  System enhancements allow that ID to represent specific programs (e.g. with specific ratings), the ID continues to identify the associated Channel.


