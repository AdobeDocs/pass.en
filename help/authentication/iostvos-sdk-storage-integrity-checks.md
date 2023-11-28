---
title: iOS/tvOS Storage Integrity Check Mechanism
description: iOS/tvOS Integrity Check Mechanism
---
# iOS/tvOS Integrity Check Mechanism {#iostvos-sdk-storage-integrity-checks}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#Intro}

Starting with version 3.8.3 of the iOS/tvOS AccessEnabler SDK, the option of performing storage integrity checks is available on AccessEnabler initialization.

In order to use this mechanism, the api was extended with an additional initialization method for the AccessEnabler class.

```
- (nonnull id) initWithStorageCheck:(IntegrityCheckType)performIntegrityCheck softwareStatement:(nonnull NSString *)softwareStatement;
```


## Integrity checks {#Checks}

The storage integrity checks are useful when corruption of the AccessEnabler storage is suspected (such as when a race condition happens during a read/write storage operation).

The following checks are available to perform on AccessEnabler initialization:
- Storage operability: checks for success on read and write operations
- Stored values integrity: checks that all values are valid and in the expected format

>[!IMPORTANT]
> 
>In case one of the checks fails, all values in the storage are cleared and the user is logged out, which may lead to a bad user experience. Use storage integrity checks only when deemed necessary.


## Default behavior {#Default}

The storage integrity checks are turned off by default when initializing AccessEnabler using the default initialization method:

```
///  SWIFT
let accessEnabler: AccessEnabler = AccessEnaler(softwareStatement)

///  Objective C
AccessEnabler *accessEnabler = [[AccessEnabler alloc] init:softwareStatement];
```

To explicitly specify which storage integrity checks to be performed on AccessEnabler initialization, use the following initialization method:

```
///  SWIFT
let accessEnabler: AccessEnabler = AccessEnabler(storageCheck: IntegrityCheckType.INTEGRITY_CHECK_ALL, softwareStatement: softwareStatement)

///  Objective C
AccessEnabler *accessEnabler = [[AccessEnabler alloc] initWithStorageCheck:INTEGRITY_CHECK_ALL softwareStatement:softwareStatement];
```


## IntegrityCheckType {#Switcher}

The IntegrityCheckType enum is exposed to the client application and has the following values:

| Value                 | Checks performed                                    | Storage cleared | Description                                                            | Recommended use case                                                                                                     |
|-----------------------|-----------------------------------------------------|-----------------|------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| INTEGRITY_CHECK_NONE  | None                                                | Never           | No integrity checks are performed on storage initialization            | When the SDK flows are working as expected                                                                               |
| INTEGRITY_CHECK_ALL   | Storage operability <br/> Validity of stored values | On check fail   | All available integrity checks are performed on storage initialization | When corruption of SDK storage is suspected. <br/> In case any of the integrity checks fail, the user will be logged out |
| INTEGRITY_CHECK_CLEAR | None                                                | Always          | The storage is cleared on storage initialization                       | When the SDK flows cannot be completed as expected                                                                       |
