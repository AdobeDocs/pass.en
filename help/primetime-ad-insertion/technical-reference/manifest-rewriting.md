---
title: Manifest Rewriting and Ad-Fetching Rules
description: Manifest Rewriting and Ad-Fetching Rules
exl-id: 3750abc1-da60-4faf-ba85-37914f33641f
---
# Manifest Rewriting and Ad-Fetching Rules {#manifest-rewriting}

Primetime Ad Insertion is capable of re-writing fragments and fetching assets using simple search/replace rules.  This can be used to down-convert https to http requests, which would increase performance by removing TLS handshakes.  This can also be used to deliver ad assets and cdn assets from the same CDN.

Rules are defined as regular expression search/replace, and can be used to transform urls prior to being sent, as well as after inserted into a manifest.

This example rule will downconvert all ad requests to domain.com from https to http.

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

The following rule will use the content CDN to deliver ads that are located on Adobe's ad storage CDN.

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

Rules can be named and enabled/disabled by modifying the `ptprotoswitch` parameter in the Bootstrap API, which is a comma separated list of rules to execute.  For example, these two rules can both be executed by setting `ptprotoswitch=adfetch_rule1,adfetch_rule2`:

```
<ruleSet>
    <rule name="rule1">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
    <rule name="rule2">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
</ruleSet>
```

Contact your technical support to create/enable these rules for your account.
