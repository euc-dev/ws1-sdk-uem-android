---
layout: page
title: App Wrapping
hide:
  #- navigation
  - toc
---

## Overview

The steps in this tutorial are done with the assumption that you have gone through the steps in [Getting Started](../getting-started.md) tutorial including the wrapping subsection.

## Requirements

- Access to AirWatch Console v7.3+
- Android v2.3+ devices

## Developer Considerations

The app developer must follow a specific regimen about what networking APIs are used in the app in order for traffic to be tunneled via wrapping. Application networking calls must be made using one of the following APIs, based on the proxy type.

### Proxy Type: F5 – Supported Components

- Covers all app level http/https communications

### Proxy Type: MAG – Supported Components

- org/apache/http/impl/client/AbstractHttpClient
- org/apache/http/impl/client/DefaultHttpClient
- org/apache/http/impl/client/ HttpClientAndroidLib
- java/net/URL l android/webkit/WebView
- android/webkit/WebViewClient

!!!Note
    The MAG supports only HTTP and HTTPS traffic, so you cannot use classes such as Socket().

## Tutorial

The app wrapping process consists of 3 main steps:

1. Policy configuration – Define the security policies you want to apply to your app. This is where the tunneling policy will be defined.
2. Wrapping the app – Provide the code signing assets required to wrap the app.
3. Assignment and Deployment – Configure the deployment rules for when the app wrapping is complete.

### Policy Configuration

At this point in the tutorial, we assume you have already gone through the steps of uploading your app and assigning the wrapping profile mentioned in General Setup.

Log into the AirWatch Console and identify if the wrapping profile you assigned to your application is the default profile or a custom profile. If there is no profile assigned, you can choose from one of two ways to configure the policy: group-wide default settings or an ad-hoc custom profile.

### Using the Default Profile (Recommended)

1. If the profile assigned is the default profile, then the policy settings can be edited by navigating to Apps & Books > All Apps & Books Settings > Apps > Settings And Policies > Security Policies.
2. Enable the AirWatch App Tunnel option.
3. Set your App Tunnel Mode to the proxy you plan on using. (If there is no proxy configured, follow the configure proxy settings link on the UI to walk through setting up your proxy)
4. Click the Save button to persist any changes you have made.

!!!Note
    These changes will reflect via the Default Profile during profile assignment which will be done in a later step in the tutorial.

### Using an Ad-hoc Custom Profile

1. Navigate to Apps & Books > All Apps & Books Settings > Apps > Settings And Policies > Profiles.
2. Select your assigned profile, or click on Add Profile and select the App Wrapping Profile.
3. In the General section, assign a name to your profile.
4. Select the Proxy payload and Enable App Tunnel and set your App Tunnel Mode to the proxy you plan on using.
5. Click Save to create or update your app wrapping profile.

### Wrapping the app

Once you have set up the appropriate configuration policies. The next step is to actually wrap the application.

1. Navigate to the Apps & Books section back on the AirWatch Console and select the list view.
2. Select the internal tab in the list view and add an application.
3. Upload the .ipa file you intend to wrap.
4. Click the “More” tab and select App Wrapping.
5. Enable app wrapping. Choose the app wrapping profile to assign to your wrapped application. (This is what you created in the Policy Configuration section above)
6. Upload your mobile provisioning profile along with its corresponding code signing certificate.
7. Once complete, click “Save and assign” to move to the next portion for deploying your app to the appropriate device smart groups.

### Assignment and Deployment
The last step is to assign who should get the app and when.

1. Click add assignment.
2. Select or create a smart group with your desired set of device assignments.
3. Configure the push mode and deployment time if applicable.
4. Add the assignment.
5. Once ready, click Save and Publish to start the wrapping and deployment process.