---
title: API Endpoints
description: Complete list of the Concurrency Monitoring APIs
exl-id: e8a9dfd2-cd16-4971-b9bc-9646987dd3ce
product_v2:
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
    internal-label: Pass
---
# API Endpoints 

## Core Session Management

| Endpoint                              | Method | Description                           |
|---------------------------------------|--------|---------------------------------------|
| `/sessions/{idp}/{subject}`           | POST   | Create a new streaming session        |
| `/sessions/{idp}/{subject}/{session}` | POST   | Send heartbeat to keep session alive  |
| `/sessions/{idp}/{subject}/{session}` | DELETE | Terminate a session                   |
| `/runningStreams/{idp}/{subject}`     | GET    | Get all active sessions for a subject |

## Metadata Management

| Endpoint    | Method | Description                                  |
|-------------|--------|----------------------------------------------|
| `/metadata` | GET    | Get required metadata fields for application |
