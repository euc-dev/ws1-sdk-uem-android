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

## Tutorial

### Enabling a passcode policy

At this point in the tutorial, we assume you have already gone through the steps of uploading your app and assigning the wrapping profile mentioned in General Setup.

Log into the AirWatch Console and identify the wrapping profile you assigned to your application is the default profile or a custom profile.

### If using the default profile

1. If the profile assigned is the default profile, then the policy settings can be edited by navigating to Apps & Books > All Apps & Books Settings > Apps > Settings And Policies > Security Policies.
2. Set Authentication Type to Passcode and configure an appropriate timeout, max number of failed attempts, and passcode complexity.
3. Once you are done, click save to enforcing the new policy.

### If using a custom profile

1. If the profile assigned is a custom profile you’ve created, then the policy settings can be edited by navigating to Apps & Books > All Apps & Books Settings > Apps > Settings And Policies > Profiles and then selecting the wrapping profile you’ve assigned to your app.
2. Edit the profile, and select the authentication payload on the left and configure an appropriate timeout, max number of failed attempts, and passcode complexity.
3. Once you are done, click save to start enforcing the new policy.

## Testing Your Application

1. Enroll your device into AirWatch if you haven’t already done so via the instructions provided in the General Setup section.
2. Once enrolled, install the wrapped application via your app catalog.
3. Launch the wrapped application and wait for the app to finish initialization.
4. You should be prompted to create a new passcode in the app if you haven’t already done so.
