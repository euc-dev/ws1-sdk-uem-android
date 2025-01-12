---
layout: page
title: Release Notes
hide:
  #- navigation
  #- toc
---

Updated on 12/20/2024

## What's in the Release Notes?

Workspace ONE SDK for Android Release Notes describe the new features and enhancements in each release. This page contains a summary of the new capabilities, issues that have been resolved, and known issues that have been reported in each release. The Workspace ONE SDK for Android allows you to enhance your enterprise applications with MDM capabilities. You can use Workspace ONE UEM powered by AirWatch features that add a layer of security and business logic to your application.

!!! warning "Important Update Starting June 2024"

    Starting June 2024 version 24.06 onwards, Workspace ONE SDK for Android will **NOT** be distributed through the [My Workspace ONE portal](https://my.workspaceone.com/products/Workspace-ONE-SDK). It will only be distributed as a maven package; developers need to follow the instructions provided in the below-mentioned link to integrate the Workspace ONE SDK Android package into their applications.

## Integration

The SDK is accessible from a Maven repository. For integration documentation, refer to [Workspace ONE SDK for Android](https://developer.omnissa.com/ws1-uem-sdk-for-android/) page in the Omnissa Developer Portal and KB article [General Availability of Workspace ONE SDK Android (6000158)](https://kb.omnissa.com/s/article/6000158).

Developers must follow the instructions in the [Public Maven Repository Integration Note](https://github.com/euc-releases/workspace-ONE-SDK-integration-samples/blob/main/IntegrationGuideForAndroid/Guides/PublicMaven/WorkspaceONE_Android_PublicMavenNote.md) to integrate the Workspace ONE SDK Android package into their applications.

Also when adding module dependencies, ensure the group and module names are in lowercase. Example: 
```c
dependencies { implementation ("com.airwatch.android:airwatchsdk:${airwatchVersion}") implementation ("com.airwatch.android:awframework:${airwatchVersion}") implementation ("com.airwatch.android:awnetworklibrary:${airwatchVersion}") }
```

## Workspace ONE SDK 24.11 for Android

### What's new
- Branding Update: SDK now features a new logo and splash screens as part of our transition to Omnissa.
- As part of rebranding transition few packageID's are updated as mentioned in the [KB article](https://kb.omnissa.com/s/article/6000713)
- Enhancements in Multi part log improvements.
- Disabled Shift Based Access feature.

### Compatibility
- Android 7.0+ (i.e., API 24)
- Workspace ONE UEM Console 2302+
- Android Studio with the Gradle Android Build System (Gradle) 7.4+
- JDK version 17
- Workspace ONE Intelligent Hub for Android version 24.10


## Workspace ONE SDK 24.10 for Android

### What's new
- Support for POST requests for sending SCEP (Simple Certificate Enrollment Protocol) requests
- Decommissioning of MAG and Standard Proxy
- Stability improvements and Bug fixes.

### Compatibility

- Android 7.0+ (i.e., API 24)
- Workspace ONE UEM Console 2302+
- Android Studio with the Gradle Android Build System (Gradle) 7.4+
- JDK version 17
- Workspace ONE Intelligent Hub for Android version 24.07

## Workspace ONE SDK 24.07 for Android

### What's new
- Stability improvements and Bug fixes.
- Third party library updates.

### Compatibility

- Android 7.0+ (i.e., API 24)
- Workspace ONE UEM Console 2302+
- Android Studio with the Gradle Android Build System (Gradle) 7.4+
- JDK version 17
- Workspace ONE Intelligent Hub for Android version 24.07

## Workspace ONE SDK 24.06.1 for Android

### What's new

- Migrated play core library to target Android API 34

## Workspace ONE SDK 24.06 for Android

### What’s new

- Stability improvements and Bug fixes.
- Third party library updates.

### Compatibility

- Android 7.0+ (i.e., API 24)
- Workspace ONE UEM Console 2212+
- Android Studio with the Gradle Android Build System (Gradle) 7.4+
- JDK version 17
- Workspace ONE Intelligent Hub for Android version 24.04

## Workspace ONE SDK 24.04 for Android

### What’s new

- Compatibility updates for targeting Android 14 (i.e., API 34)
- Support for Android 5 and 6 has been discontinued.
- Bug fixes and stability improvements.
- Third party library updates.

### Compatibility

- Android 7.0 + (i.e., API 24)
- Workspace ONE UEM Console 2212+
- Android Studio with the Gradle Android Build System (Gradle) 7.4 +
- JDK version 17
- Workspace ONE Intelligent Hub for Android version 24.01

## Workspace ONE SDK 24.01 for Android - February 2024

### New Features

- We upgraded SQL Cipher from 4.5.4. to 4.5.6.  
  
  Workspace ONE SDK 24.01 for Android has upgraded the SQLCipher library (https://www.zetetic.net/sqlcipher/sqlcipher-for-android/) from 4.5.4 to 4.5.6 version. To consume SDK 24.01, upgrade the integrating application SQLCipher library version to a minimum of 4.5.5.

- Fixed minor bugs and improved stability.

### Minimum Requirements

Minimum requirements for Workspace ONE SDK 24.01 for Android:

- Android 5.0 and later
- API Level 21 and later
- Workspace ONE UEM Console 2206 and later
- Android Studio with the Gradle Android Build System (Gradle) 3.3.0 and later
- Workspace ONE Intelligent Hub for Android version 23.11

### Resolved Issues

We are always working to improve Workspace ONE SDK for Android with every release. There are no major bug fixes to report.

### Known Issues

We haven't identified any notable known issues in this release. If you have any problems, reach out to our support team.

## Workspace ONE SDK 23.12 for Android - December 2023

### New Features

- Updated third-party libraries.
- Fixed minor bugs and improved stability.

### Minimum Requirements

Minimum requirements for Workspace ONE SDK 23.12 for Android:

- Android 5.0 and later
- API Level 21 and later
- Workspace ONE UEM Console 2206 and later
- Android Studio with the Gradle Android Build System (Gradle) 3.3.0 and later
- Workspace ONE Intelligent Hub for Android version 23.11

### Resolved Issues

We are always working to improve Workspace ONE SDK for Android with every release. There are no major bug fixes to report.

### Known Issues

We haven't identified any notable known issues in this release. If you have any problems, reach out to our support team.

## Workspace ONE SDK 23.10 for Android - November 2023

### New Features

- Fixed minor bugs and improved stability.
- Updated third-party libraries.

### Minimum Requirements

Minimum requirements for Workspace ONE SDK 23.10 for Android:

- Android 5.0 or later
- API Level 21 or later
- Workspace ONE UEM Console 2206 or later
- Android Studio with the Gradle Android Build System (Gradle) 3.3.0 or later
- Workspace ONE Intelligent Hub for Android version 23.08 or later

### Resolved Issues

We are always working to improve Workspace ONE SDK for Android with every release. There are no major bug fixes to report.

### Known Issues

We haven't identified any notable known issues in this release. If you have any problems, reach out to our support team.
