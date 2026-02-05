---
title: Handling 409 Conflict Errors
description: Learn how to handle 409 Conflict errors when concurrent usage limits are reached
exl-id: 23a73e48-8ae0-4e0e-85db-dfc09d1386a7
---
# Handling 409 Conflict Errors {#handling-409-errors}

When a user tries to start a new stream and hits a concurrent usage limit, Concurrency Monitoring returns a **409 Conflict** response. Understanding how to handle this error is crucial for providing a good user experience.

## What is a 409 Conflict? {#what-is-a-409-conflict}

A 409 Conflict occurs when:

1. **User tries to start a new stream**
2. **Policy evaluation determines** the request would exceed limits
3. **System returns 409** with detailed conflict information
4. **Application must decide** how to handle the conflict

### 409 Response Structure

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
        "id": "advice-1",
        "adviceType": "rule-violation",
        "attributes": {
          "rule": "max_streams",
          "threshold": 3,
          "current": 4,
          "conflicts": [
            {
              "sessionId": "session-123",
              "terminationCode": "term-456",
              "metadata": {
                "deviceId": "device-789",
                "channel": "Channel1",
                "contentType": "live"
              }
            }
          ]
        }
      }
    ]
  }
}
```

## Understanding the Response {#understanding-the-response}

### Key Fields

- **`decision`**: Always "DENY" for 409 conflicts
- **`associatedAdvice`**: Array of advice objects explaining the violation
- **`conflicts`**: List of active sessions that are causing the conflict
- **`terminationCode`**: Unique code to terminate a specific session

### Advice Types

#### Rule Violation Advice

```json
{
  "adviceType": "rule-violation",
  "attributes": {
    "rule": "max_streams",
    "threshold": 3,
    "current": 4,
    "conflicts": [...]
  }
}
```

#### Remote Termination Advice

```json
{
  "adviceType": "remote-termination",
  "attributes": {
    "terminatedBy": "session-456",
    "reason": "New session requested with X-Terminate header"
  }
}
```

## Handling Strategies {#handling-strategies}

- In FIFO mode, CM allows the new session to start by terminating an existing one.
- In LIFO mode, CM blocks the new session and informs the user


## Best Practices {#best-practices}

### 1. Clear User Communication

- **Explain the limit** - Users should understand why they're blocked
- **Show available options** - What they can do to resolve the conflict
- **Provide context** - Show which sessions are active

### 2. Graceful Error Handling

- **Don't crash** - Handle 409 errors gracefully
- **Provide alternatives** - Offer ways to resolve the conflict
- **Save user state** - Don't lose their content selection

### 3. User Experience Considerations

- **Quick resolution** - Make it easy to resolve conflicts
- **Clear choices** - Users should understand their options
- **Consistent behavior** - Handle conflicts the same way every time

### 4. Technical Considerations

- **Parse response carefully** - Extract all relevant information
- **Handle edge cases** - What if no conflicts are returned?
- **Log conflicts** - Track policy violations for analysis
