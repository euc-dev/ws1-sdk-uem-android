---
layout: page
title: Airwatch SDK
hide:
  #- navigation
  - toc
---

## Overview

The steps in this tutorial are done with the assumption that you have gone through the steps in [Getting Started](../getting-started.md) tutorial as well as Integrating the Client SDK portion in the [SDK Setup](../SDK-Setup.md) section.

!!!Important
    You will need to download the SDK binary separately via [resources.air-watch.com](https://resources.air-watch.com/). Please contact your Omnissa representative or support to gain access.

## Requirements

- Android 7.0+ (i.e., API 24)
- Workspace ONE UEM Console 2302+
- Android Studio with the Gradle Android Build System (Gradle) 7.4+
- JDK version 17
- Workspace ONE Intelligent Hub for Android version 24.07
- Android Test Device
- AirWatch SDK from the Resources Portal

## Tutorial

### Step 1: Integrate the AirWatch SDK

Follow the [instructions to integrate the AirWatch Software Development Kit (SDK) for Android](../SDK-Setup.md) into your application if you haven’t already done so.

### Step 2: Add Custom Settings in your SDK profile

For this next part, you will need to check which profile you have assigned to your SDK app. You can do this by navigating to Apps & Books > Details View. Click Edit. Choose More > SDK. Check what profile is assigned for SDK Profile.
![](./a8000389-bd0d-4f35-b343-8031dbdc67d4)

#### Using the Default SDK Profile (Recommended)

1. If the profile assigned is the default profile, then the policy settings can be edited by navigating to Apps & Books > All Apps & Books Settings > Apps > Settings And Policies > Settings.
2. Enable the custom settings and add your custom settings. This is a string field and can contain XML, JSON, or plain text. You can also insert lookup values if desired.
![](./0f6e3878-664c-4e51-a289-0d1e5153ceb8)
3. Once you are done, click save to start enforcing the new policy.

#### Using a custom profile

1. In the *AirWatch Console, Choose Apps & Books > All Apps & Books Settings.
2. Choose Settings and Policies > Profiles and click Add Profile to create a custom profile or edit an already existing profile currently assigned to your app.
![](./6e5a2fef-d552-42d2-9f1d-2051c98499b7)
3. You will be asked to Choose SDK Profile or Application Profile. Select the SDK profile.
4. Choose Android and fill in the Name field on the General Tab.
![](./582fc9d5-3d56-4963-bd59-0fba9c9d479c)
5. Click Custom Settings on the left, and add your custom settings. This is a string field and can contain XML, JSON, or plain text. You can also insert lookup values if desired.
![](./6462ed6a-3af9-4f82-b134-5498d4d6fc3f)
6. Save the Profile.

### Step 3: Retrieving the Profile within Your Application

The code to retrieve these settings within the app is very simple if SDK integration is already done from Step 1:

```JAVA
SDKManager mgr = SDKManager.init(activity);
String customSettings = mgr.getCustomSettings();
```

Here is a screenshot from the debugger showing the sample XML settings entered in the AirWatch Console above:
![](./64620e80-17a2-4016-af0f-f7e81a88b65f)

Use these settings however you wish in your app!
