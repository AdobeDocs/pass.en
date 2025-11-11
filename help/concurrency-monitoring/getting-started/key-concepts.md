---
title: Key Concepts
description: Learn the fundamental concepts of Concurrency Monitoring including sessions, policies, metadata, and more
---

# Key Concepts {#key-concepts}

Understanding the core concepts of Concurrency Monitoring is essential for successful implementation. This guide explains the fundamental building blocks and how they work together.

## Core Concepts {#core-concepts}

### Sessions

A **session** represents an active video streaming instance. Think of it as a "ticket" that allows a user to watch content.

#### Session Lifecycle

1. **Creation** - When user starts watching content
2. **Active** - While user is watching (maintained by heartbeats)
3. **Termination** - When user stops watching or session expires

#### Session Properties

```json
{
  "sessionId": "unique-session-identifier",
  "idp": "identity-provider",
  "subject": "user-identifier",
  "startTime": "2024-01-15T10:30:00Z",
  "expiresAt": "2024-01-15T10:40:00Z",
  "metadata": {
    "deviceId": "device-123",
    "channel": "Channel1",
    "contentType": "live"
  }
}
```

### Policies

**Policies** are business rules that define limits and restrictions for concurrent streaming. They determine when users can start new streams.

#### Policy Components

- **Rules** - Specific limits and conditions
- **Metadata Requirements** - What data is needed
- **Evaluation Logic** - How the policy is applied

#### Example Policy

```json
{
  "name": "basic_stream_limit",
  "description": "Maximum 3 concurrent streams per user",
  "rules": [
    {
      "type": "maxstreams",
      "limit": 3,
      "message": "You have reached your maximum of 3 concurrent streams"
    }
  ]
}
```

### Metadata

**Metadata** provides context about each session. It includes information about the device, content, user, and application.

#### Metadata Categories

| Category        | Examples                                 | Purpose                         |
|-----------------|------------------------------------------|---------------------------------|
| **Device**      | `deviceId`, `deviceType`, `osName`       | Identify and categorize devices |
| **Content**     | `channel`, `contentType`, `assetId`      | Describe what's being watched   |
| **User**        | `subject`, `subscriptionTier`            | User-specific information       |
| **Application** | `applicationName`, `applicationPlatform` | App-specific details            |
| **Location**    | `country`, `hba`                         | Geographic and network info     |

#### Required vs Optional Metadata

- **Required metadata** - Must be provided for session creation
- **Optional metadata** - Can be provided for enhanced policies
- **Standard metadata** - Predefined fields available to all applications
- **Custom metadata** - Application-specific fields you define

## Identity and Authentication {#identity-and-authentication}

### Identity Provider (IdP)

An **Identity Provider** is the service that authenticates users and provides their identity information. In Adobe Pass integration, this is typically an MVPD.

#### IdP Examples

- Cable companies (Comcast, Charter, etc.)
- Satellite providers (DirecTV, Dish)
- Streaming services (Netflix, Hulu)
- Mobile carriers (Verizon, AT&T)

### Subject

A **subject** is the unique identifier for a user within an Identity Provider. This is typically the user's account ID or subscriber ID.

## Session Management {#session-management}

### Heartbeats

**Heartbeats** are periodic API calls that keep sessions active. They tell the system "this user is still watching."

#### Heartbeat Requirements

- **Frequency** - Every 60 seconds (recommended)
- **Purpose** - Keep session alive, update metadata
- **Termination** - Session expires if heartbeats stop


### Session Termination

Sessions can be terminated in several ways:

1. **User stops watching** - Application calls DELETE endpoint
2. **Session expires** - No heartbeat received within timeout
3. **Policy violation** - New session terminates old one (FIFO)
4. **Remote termination** - Another device terminates the session

## Policy Evaluation {#policy-evaluation}

### How Policies Work

1. **User requests new stream**
2. **System evaluates policies** against current usage
3. **Decision made** - Allow or deny
4. **Response sent** - Success or conflict information

## Conflict Resolution {#conflict-resolution}

### What is a Conflict?

A **conflict** occurs when a user tries to start a new stream but would exceed their limits.

### Conflict Response

When a conflict occurs, the system returns a 409 Conflict response with detailed information:

```json
{
  "status": "error",
  "error": {
    "code": "POLICY_VIOLATION",
    "message": "Concurrent usage limit exceeded"
  },
  "evaluationResult": {
    "decision": "DENY",
    "associatedAdvice": [
      {
        "adviceType": "rule-violation",
        "attributes": {
          "rule": "max_streams",
          "threshold": 3,
          "current": 4,
          "conflicts": [
            {
              "sessionId": "session-123",
              "terminationCode": "term-456",
              "metadata": {...}
            }
          ]
        }
      }
    ]
  }
}
```

### Resolution Strategies

#### LIFO (Last In, First Out)

- **Old sessions are protected**
- **New session is blocked**
- **Simpler UI**
- **Better for extended viewing**


#### FIFO (First In, First Out)

- **New session terminates an existing one**
- **User chooses which session to stop**
- **More complex UI required**
- **Better for content switching**

## Applications and Tenants {#applications-and-tenants}

### Application

An **application** is a software program that integrates with Concurrency Monitoring. Each application has a unique ID and can have its own policies.

#### Application Examples

- Mobile app (iOS/Android)
- Web application
- Smart TV app
- Set-top box application

### Tenant

A **tenant** is an organization that owns one or more applications. Tenants can share policies across applications.

#### Tenant Structure

```
Tenant: "Streaming Company"
├── Application: "Mobile App"
├── Application: "Web App"
└── Application: "TV App"
```

## Environments {#environments}

### Staging Environment

- **Purpose** - Development and testing
- **URL** - `https://streams-stage.adobeprimetime.com/v2/`
- **Credentials** - Test application IDs
- **Data** - Test data only

### Production Environment

- **Purpose** - Live user traffic
- **URL** - `https://streams.adobeprimetime.com/v2/`
- **Credentials** - Production application IDs
- **Data** - Real user data

## Integration Flow {#integration-flow}

### Basic Flow

1. **User Authentication** - Authenticate with Adobe Pass
2. **Session Creation** - Create CM session with user metadata
3. **Heartbeat Management** - Send periodic heartbeats
4. **Session Termination** - Terminate when user stops watching

### Error Handling

1. **404 Not Found** - Handle requests with session ID not generated by CM service 
2. **409 Conflicts** - Handle policy violations
3. **410 Gone** - Handle session termination
4. **Network Errors** - Handle connectivity issues
5. **Authentication Errors** - Handle credential issues


## Common Terminology {#common-terminology}

| Term            | Definition                                 |
|-----------------|--------------------------------------------|
| **Session**     | Active video streaming instance            |
| **Policy**      | Business rule defining usage limits        |
| **Metadata**    | Contextual information about sessions      |
| **IDP**         | Identity Provider (authentication service) |
| **Subject**     | User identifier within an IDP              |
| **Heartbeat**   | Periodic call to keep session active       |
| **Conflict**    | Policy violation when starting new stream  |
| **LIFO**        | Last In, First Out conflict resolution     |
| **FIFO**        | First In, First Out conflict resolution    |
| **Tenant**      | Organization owning applications           |
| **Application** | Software program using CM                  |

