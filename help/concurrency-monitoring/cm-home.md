---
title: Concurrency Monitoring Introduction
description: Concurrency Monitoring Introduction
exl-id: 725cc64b-6b03-46e3-a038-41e9b1341c6b
---
# Concurrency Monitoring Introduction {#intro}

Concurrency Monitoring is a service that enables content providers and identity providers  (MVPDs and Programmers) to define and enforce limits on concurrent video streaming across multiple applications, devices, and platforms. Whether you're a programmer looking to control how many streams a subscriber can watch simultaneously, or an MVPD wanting to enforce usage policies across your content partners, Concurrency Monitoring provides the tools you need.

## What is Concurrency Monitoring? {#what-is-cm}

Concurrency Monitoring is a centralized service that tracks and manages active video streaming sessions in real-time. It allows you to:

- **Limit concurrent streams per subscriber** - Control how many simultaneous video streams a user can access
- **Enforce device restrictions** - Limit streaming to specific device types or quantities
- **Implement location-based policies** - Restrict streaming based on geographic location
- **Create content-specific rules** - Apply different limits for live vs. VOD content
- **Monitor usage patterns** - Gain insights into how your content is being consumed

## How It Works {#how-it-works}

Concurrency Monitoring operates through a simple but powerful API:

1. **Session Initialization** - When a user starts watching content, your application creates a session
2. **Policy Evaluation** - The service evaluates your defined policies against current usage
3. **Real-time Monitoring** - Heartbeat calls keep sessions active and monitor compliance

## New to Concurrency Monitoring? {#new-to-cm}

Start with our [Getting Started Guide](getting-started/getting-started-overview.md) to understand the basics and set up your first integration.

