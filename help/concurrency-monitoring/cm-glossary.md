---
title: Glossary
description: Glossary of terms in Concurrency Monitoring
exl-id: 3b3b36fe-9f04-4de9-bd84-9f8d766bbc71
---
# Glossary {#glossary}

## Account ID {#accid-defn}

* MVPD account of a subscriber, usually corresponding to the actual billing account. This account must be identifiable by the MVPD in its own system.

## Action {#action-defn}

* The type of access that the subject requests; the possible values for CM are ***initiate*** or ***continue*** a streaming session.

## Active stream {#active-stream-defn}

* A stream that has received at least 1 event (heartbeat) in the last 90 seconds.

* ***Note:*** If the last event in the stream is of type stop (`?event=stop`), it will not be counted. This is an optimization that allows a player to explicitly close a stream so that it's not considered "active" anymore.

## Application {#application-defn}

* Developed by the Tenant for video content access
* Makes and enforces decisions about content access based on information provided by the Concurrency Monitoring Service (this is valid in the [Policy Information Point](/help/concurrency-monitoring/policy-info-pt-versionone.md) case)
* Will have a unique **application ID** provided by Adobe.

## Concurrency Monitoring Service {#cm-service-defn}

* Acts as a monitoring system for the subscribers, supporting the MVPDs and Programmers in their cross-application policy enforcement requirements.
* Receives heartbeats that indicate stream activity.
* Acts as a _Policy Decision Point_ by evaluating authorization requests based on user activity and providing an allow/deny response.
* Acts as a _Policy Information Point_ by reporting the number of active streams (and additional stream metadata) for a subscriber.
 
## Environment {#env-defn}

* Additional information relevant for the request, like configuration settings or system time.

## MVPD {#mvpd-defn}

* Multichannel Video Programming Distributor.
* Acts as Authentication and Authorization Provider, but can also be Service or Content Provider.

## Policy {#policy-defn}

* The core access control concept in CM defined as a target and one or more rules grouped under a unique name.

## Policy Administration Point (PAP) {#policy-admin-pt-defn}

* Point which manages access authorization policies. This will not be documented here, but eventually we are going to provide a self-service console for customers to manage their access policies.

## Policy Decision Point (PDP) {#policy-decn-pt-defn}

* Point which evaluates access requests against authorization policies before issuing access decisions.

## Policy Enforcement Point (PEP) {#policy-ef-pt-defn}

* Point which intercepts user's access request to a resource, makes a decision request to the PDP and enforces that decision on the request. This is currently the client application and there is no plan of transferring this role to Concurrency Monitoring.

## Policy Information Point (PIP) {#policy-info-pt-defn}

* A source of attribute values. Concurrency Monitoring acts as an information point by providing:
    * pass-through stream metadata.
    * activity metrics regarding the concurrent streams.

## Programmer {#programmer-defn}

* Acts as a Service and Content provider.
* Relies on the deployed client application that integrates with Concurrency Monitoring service to enforce the defined security policies based on the above mentioned service data.
* Needs to support the MVPD in collecting subscriber activity and enforcing the limiting rules when on their properties.
* May also be interested in limiting concurrent access to their content across all destination portals, as a separate rule.

    *Q: Why Programmer and not Requestor ID like in the rest of Adobe Pass Authentication?*

    *A: The reason is to allow Programmers to use this parameter flexibly to pass or isolate data between their properties depending on their use cases.*

## Resource {#resource-defn}

* The actual content that a subject wants to consume. The resource usually carries attributes related to the owner (publisher) and may also provide extra information like genre or whatever.

## Rule {#rule-defn}

* A boolean function that is evaluated against a particular stream and the relevant user activity in order to determine whether access should be allowed or denied for that stream.

## Streaming Session {#streaming-session-defn}

* A streaming video session initiated by a subject for consuming a specific resource.

## Subject {#subj-defn}

* The consumer of the (video) content over the internet. We are deliberately avoiding the term _**user**_, as Concurrency Monitoring usually deals with MVPD account IDs (which involve several actual users sharing the same contract, for example family members for a household).

* For each stream, the subject can be enhanced with attributes related to the actual person using the service, their network connected device and so on.

## Subscriber {#subscriber-defn}

* The paying customer of an MVPD or a person who shares the credentials of a paying customer
* Can be stopped from watching content by the Concurrency Monitoring Service, by the client application using the above mentioned service.
* In the best case scenario, he or she never notices the existence of the Concurrency Monitoring Service

## Target {#target-defn}

* A stream predicate that will return whether the rule is applicable to a given stream. The implicit target in CM will be be any stream created by an application which references the policy in question. Additionally, attribute value conditions can be added in order to fine-tune the activity filtering before applying the rules.

## Tenant {#tenant-defn}

* A Concurrency Monitoring customer's organization.
