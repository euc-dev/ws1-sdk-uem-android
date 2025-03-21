---
layout: page
title: Airwatch SDK Setup
hide:
  #- navigation
  - toc
---

## Overview

The steps in this tutorial are NOT required if you are using App Wrapping or using only approaches from AppConfig.org. This tutorial will walk developers through how to setup the core SDK framework for those who have chosen the SDK approach.

Before moving forward to the SDK setup tutorial, ensure you have completed the instructions in the [Getting Started](getting-started.md) tutorial and uploaded your app with an assigned SDK profile.

!!! warning "Important Update Starting June 2024"

    Starting June 2024 version 24.06 onwards, Workspace ONE SDK for Android will **NOT** be distributed through the My Workspace ONE portal. 
    
The SDK is accessible from a Maven repository. For integration documentation, please follow the instructions in the [Public Maven Repository Integration Note](https://developer.omnissa.com/ws1-sdk-for-android/guides/WorkspaceONE_Android_PublicMavenNote.pdf), and KB article [General Availability of Workspace ONE SDK Android (6000158)](https://kb.omnissa.com/s/article/6000158) to integrate the Workspace ONE SDK Android package into their applications.

## Requirements

- Android 7.0+ / Oreo / API Level 24+
- Android Studio with the Gradle v8.2.2+
- Android Test Device
- AirWatch SDK from the Resources Portal
- Workspace ONE Intelligent Hub v23.06+ for Android (Requirement be lower depending on features used)

## Tutorial

There are three components in the Android SDK:

- Client SDK – This is a lightweight JAR file which contains a basic level of functionality.
- AWFramework – This is a more advanced AAR file which contains the logic for features such as app tunneling and integrated authentication. Integrating AWFramework also requires integration of the Client SDK.
- AWNetwork – This is a next level library which enables the networking capabilities in SDK such as tunneling of application data, NTLM and basic authentication, and certificate-based authentication. Integrating AWNetwork also requires integration of the AWFramework.

Refer to the SDK implementation guide included in your SDK package for more details on what is in the Client SDK vs. the AWFramework.

## Integrating the Workspace ONE SDK

Refer to [index](index.md) Integration guides section for instructions on how to integrate your Android app with Workspace ONE.

### Configure the App theme to have the Branding Icon

Set the SDK Branding Icon to be the image. This can be the app icon or an image specific to the app. The Branding Icon is required for SDK Login Flow integrations.
Please follow the instructions in the [Workspace ONE for Android Branding Integration Guide](https://developer.omnissa.com/ws1-sdk-for-android/guides/WorkspaceONE_Android_Branding.pdf)
to set the SDK branding icon.

## Debug Your Application

Before you can begin using the SDK API, you must ensure your application signing key is whitelisted with your AirWatch Admin Console. There are a few ways to do this depending on your deployment scenario.

## Internal Deployment or Testing

1. Sign an APK file with the debug keystore of Android Studio. This is located in ~/.android/debug.keystore by default.
2. Upload the APK file signed with your debug key to the AirWatch Admin Console. (Refer back to the Uploading your application in the [Getting Started](getting-started.md) section.)
3. Install the application through the AirWatch Agent app. This can be done by pushing the app down using the Agent‘s app catalog. If you set your installation policy to Automatic then the app will install automatically.
4. Once the app is listed in the Managed Apps section of the Agent, it is ready for local management and can then be sideloaded manually through your IDE (Android Studio).

## Play Store Deployment

For applications that are deployed publicly through the Play Store, send the public signing key of the application to AirWatch for whitelisting.

!!!Note
    Contact your professional services representative for the process of whitelisting the public signing key.

## Next Steps

Once the SDK setup is completed, move on to the next SDK sections to implement the feature specific logic.
