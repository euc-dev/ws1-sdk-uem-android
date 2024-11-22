---
layout: page
title: AppConfig.org
hide:
  #- navigation
  - toc
---

## Overview

This tutorial will walk developers through how to create a tunnel for a mobile app’s network traffic to access intranet resources by utilizing the Android per-app-VPN capability as prescribed by the AppConfig.org standard. The steps in this tutorial are done with the assumption that you have gone through the steps in [Getting Started](../getting-started.md) tutorial.

# Requirements

- Android 7.0+ (i.e., API 24)
- Workspace ONE UEM Console 2302+
- Android Studio with the Gradle Android Build System (Gradle) 7.4+
- JDK version 17
- Workspace ONE Intelligent Hub for Android version 24.07
- AirWatch Tunnel or a Per App VPN Solution supported by AirWatch
- Android Tunnel client application

## Developer Considerations

No additional code is required to leverage Per-app VPN. The app must be deployed under “management” to the device by AirWatch. During distribution, AirWatch entitles the application to be an approved user of the Per-App VPN utilized.

## Tutorial

Per-app VPN configuration is setup via the following steps:

1. Infrastructure configuration – Per-app VPN infrastructure is installed and configured.
2. Profile configuration – Per-app VPN profile is configured via the AirWatch Console
3. App deployment/configuration – The application is added to the AirWatch Console and the Per-app VPN profile is assigned to the application

### Infrastructure Configuration

This tutorial assumes that the Per-app VPN infrastructure is in place already. For information on AirWatch tunnel please refer to Installation and Admin guides on the myAirWatch Resource portal.

A VPN Client application is required on the Android Device. AirWatch Tunnel servers have an Android companion app that needs to be deployed.

### Profile Configuration

Log into the AirWatch console and navigate to Devices > Profiles > List View
![](./5ecd3980-e801-4412-a593-74612e4f9d28)

- Click Add then add profile
  
![](./92085076-9b70-44e2-bb90-085a8f573978)

- Select Android

![](./24d4fd40-d9af-42eb-94b0-7232e9a326c5)

- Select VPN and click Configure

![](./d2c5e4db-c7da-4160-9a59-4a33bcfae4fc)

- Select the VPN Connection type. AirWatch tunnel is selected for the Tutorial.

![](./fbab9ab3-2b71-44a2-9cd5-b95679732a02)
![](./aafaf476-ab70-4ee5-9583-f9b074fbfbc1)
![](./911a6c42-aff9-4286-9804-ba34d48b5add)

- Click Save & Publish

### App Deployment & Configuration

For this tutorial, Dolphin Browser will receive the Per-app VPN profile

- Log into the AirWatch console and navigate to Apps & Books
appsbooks

![](./cd10e8b7-4e78-4484-8e39-49f599edf793)

- Select the Public Tab and click Add Application

![](./6381c1c6-8158-452c-b2fa-66303f0b1331)

- Select the Platform and enter the name of the application platform

![](./77179364-8037-4e6d-9ea0-22c23cf84f27)

- Select Dolphin
- Select the assignment tab and assign the app to the desired Smart Group(s)

![](./8d790ed1-c77f-4933-be1b-874c54cbe99b)

- Select the Deployment Tab
- Check the “Use VPN” box and select the VPN Profile from the drop down deployment

![](./f6d1badc-6c8e-43dd-b96d-36962fe3b07a)

- Click Save and Publish
- Verify device assignment
- Click Publish to confirm settings
