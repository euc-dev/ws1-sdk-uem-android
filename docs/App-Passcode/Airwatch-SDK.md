---
layout: page
title: Airwatch SDK
hide:
  #- navigation
  - toc
---

## Overview

The steps in this tutorial are done with the assumption that you have gone through the steps in [Getting Started](../getting-started.md) tutorial as well as Integrating the Client SDK portion in the [SDK Setup](../SDK-Setup.md) section.


## Requirements

- Android 8.0+ (i.e., API 26)
- Workspace ONE UEM Console 2302+
- Android Studio with the Gradle Android Build System (Gradle) 8.2.2+
- JDK version 17
- Workspace ONE Intelligent Hub for Android version 24.07
- Android Test Device
- AirWatch SDK from the Resources Portal

## Tutorial

Integrating a SDK passcode is very simple. At the most basic level, the developer needs to interact with one class, the `SDKManager`. A common use would be to call `SDKManager.init(activity)` and then `SsoSessionReturnCode code = SDKManager.validateSSOSession(activity);` within a background thread in the `onResume()` method of your activity.

In an app with numerous Activity instances though, it proves more practical to create a new base class and do the implementation there. Below is a simple AWSDKHelper class that encapsulates the SSO validation.

```JAVA
package com.sample.sdkactivity;

import android.app.Activity;
import android.util.Log;

import com.airwatch.sdk.AirWatchSDKException;
import com.airwatch.sdk.SDKManager;
import com.airwatch.sdk.SsoSessionReturnCode;

public class AWSDKHelper {

    private static String TAG = "AWSDKHelper";

    public interface AWSDKCallback {

        public void onSSOValidateStart();
        public void onSSOValidateSuccess();
        public void onSSOValidateFailure(SsoSessionReturnCode status);
        public void onSSOValidateComplete();
    }

    public static void checkSSOSession(final Activity activity, final AWSDKCallback callback)
    {
        if ( callback != null )
        {
            Log.d(TAG, "onSSOValidateStart");
            callback.onSSOValidateStart();
        }

        new Thread(new Runnable() {
            @Override
            public void run() {
                try
                {
                    SDKManager.init(activity);
                    SsoSessionReturnCode code = SDKManager.validateSSOSession(activity);

                    if ( callback != null )
                    {
                        if ( code == SsoSessionReturnCode.SUCCESS ||
                                code == SsoSessionReturnCode.AUTH_IN_PROGRESS  )
                        {
                            Log.d(TAG, "onSSOValidateSuccess");
                            callback.onSSOValidateSuccess();
                        }
                        else
                        {
                            Log.d(TAG, "onSSOValidateFailure");
                            callback.onSSOValidateFailure(code);
                        }
                        Log.d(TAG, "onSSOValidateComplete");
                        callback.onSSOValidateComplete();
                    }
                }
                catch (AirWatchSDKException err)
                {
                    throw new RuntimeException("SDK Initialization should not fail but did!");
                }
            }
        }).start();
    }
}
```

Once this class is declared, it can be used in a simple way within a base Activity class. You can customize the `AWSDKCallback` implementation if desired to add additional behavior such as a progress dialog. Here is a simple example:

```JAVA
package com.sample.sdkactivity;

import android.app.DialogFragment;
import android.os.Bundle;
import android.os.Handler;
import android.support.v7.app.AppCompatActivity;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ProgressBar;
import android.widget.TextView;

import com.airwatch.sdk.SsoSessionReturnCode;
import com.airwatch.sdksampleapp.R;
import com.sample.sdkactivity.AWSDKHelper.AWSDKCallback;

public class BaseSDKActivity extends AppCompatActivity {

    private AWSSOLoginDialog loginDialog;

    @Override
    protected void onResume() {
        super.onResume();

        // @TODO Replace this implementation as needed with customizations for your app
        AWSDKHelper.checkSSOSession(this, new AWSDKCallback() {
            @Override
            public void onSSOValidateStart() {
                loginDialog = new AWSSOLoginDialog();
                getFragmentManager().beginTransaction().add(loginDialog, "Checking").commit();
            }

            @Override
            public void onSSOValidateSuccess() {
                getFragmentManager().beginTransaction().remove(loginDialog)
                        .commitAllowingStateLoss();
            }

            @Override
            public void onSSOValidateFailure(SsoSessionReturnCode status) {

                if (status == SsoSessionReturnCode.SSO_MODE_DISABLED) {
                    loginDialog.setError(getString(R.string.sdk_no_sso_error));
                } else {
                    loginDialog.setError(getString(R.string.sdk_generic_error));
                }
            }

            @Override
            public void onSSOValidateComplete() {
            }
        });

    }

    // Helper class for showing a progress dialog during SDK initialization
    public static class AWSSOLoginDialog extends DialogFragment {

        private TextView dialogMessage;
        private ProgressBar progressBar;

        @Override
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setStyle(STYLE_NO_FRAME, android.R.style.Theme_Holo_Light);
        }

        public void setError(final String message) {
            Handler mainHandler = new Handler(getActivity().getMainLooper());
            mainHandler.post(new Runnable() {
                @Override
                public void run() {
                    dialogMessage.setText(message);
                    progressBar.setVisibility(View.GONE);
                }
            });
        }

        @Override
        public View onCreateView(LayoutInflater inflater,
                ViewGroup container, Bundle savedInstanceState) {
            View view = inflater.inflate(R.layout.fullscreen_progress_dialog, container, false);
            dialogMessage = (TextView) view.findViewById(R.id.dialogMessage);
            progressBar = (ProgressBar) view.findViewById(R.id.progressBar);
            return view;
        }
    }
}
```

As you can see, this adds a DialogFragment that acts as a splash screen during SDK initialization. Having an Activity base class with all the SSO capability built-in makes using the SDK very easy afterward. You might implement in your `MainActivity` like this:

```JAVA
package com.sample;

...

import com.sample.sdkactivity.BaseSDKActivity;

public class MainActivity extends BaseSDKActivity {

    ...

}
```

In this example, the only customization required is to change the base class from Activity or `AppCompatActivity` to `BaseSDKActivity`. Once SSO is enabled in the AirWatch console, this app is now enabled with a PIN.

## Debug Your Application

Your application is now protected with a passcode! If you find that you are not seeing an SSO passcode, ensure that the Organization Group has Single Sign On enabled and that an Authentication Type is set as shown below:
