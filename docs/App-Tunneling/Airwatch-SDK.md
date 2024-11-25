---
layout: page
title: Airwatch SDK Setup
hide:
  #- navigation
  - toc
---

## Overview

The steps in this tutorial are done with the assumption that you have gone through the steps in [Getting Started](../getting-started.md) tutorial as well as Integrating the Client SDK portion in the [SDK Setup](../SDK-Setup.md) section.

!!!Important
    You will need to download the SDK binary separately via [resources.workspaceone.com](https://resources.workspaceone.com). Please contact your AirWatch representative or support to gain access.

## Requirements

- Android 7.0+ (i.e., API 24)
- Workspace ONE UEM Console 2302+
- Android Studio with the Gradle Android Build System (Gradle) 7.4+
- JDK version 17
- Workspace ONE Intelligent Hub for Android version 24.07
- Android Test Device
- AirWatch SDK from the Resources Portal

## Developer Considerations

In order to redirect your application’s traffic to an AirWatch supported proxy such as the Mobile Access Gateway (MAG) within the Unified Access Gateway (UAG), you can use the following AirWatch networking classes:

- AWHttpClient
- AWWebView
- AWWebViewClient

Each one of these classes is an extension of their respective base Android networking class (e.g. AWHTTPClient is a subclass of DefaultHttpClient). No additional logic is needed to handle the tunneling of a network request from your internal application.

## Tutorial

Proxy configuration with the AirWatch Android SDK is setup via the following steps:

1. Policy configuration – Tunnel profile is configured via the AirWatch Console.
2. Logic Implementation – Connect to an endpoint in your application using one of the supported networking classes
3. Assignment and Deployment – Configure the assignment and deployment rules for your organization’s devices.

### Policy Configuration

At this point in the tutorial, we assume you have already gone through the steps of uploading your app and assigning the wrapping profile mentioned in General Setup.

Log into the AirWatch Console and identify if the wrapping profile you assigned to your application is the default profile or a custom profile. If there is no profile assigned, you can choose from one of two ways to configure the policy: group-wide default settings or an ad-hoc custom profile.

#### Using the Default Profile (Recommended)

1. If the profile assigned is the default profile, then the policy settings can be edited by navigating to Apps & Books > All Apps & Books Settings > Apps > Settings And Policies > Security Policies.
settings
![](./25c216b5-d2ab-4cc3-8f29-3a32ca3a23a8)

2. Enable the AirWatch App Tunnel option.
3. Set your App Tunnel Mode to the proxy you plan on using. (If there is no proxy configured, follow the configure proxy settings link on the UI to walk through setting up your proxy)
4. Click the Save button to persist any changes you have made.

!!!Note
    These changes will reflect via the Default Profile during profile assignment which will be done in a later step in the tutorial.

#### Using an Ad-hoc Custom Profile

1. Navigate to Apps & Books > All Apps & Books Settings > Apps > Settings And Policies > Profiles.
2. Select your assigned profile, or click on Add Profile and select the App Wrapping Profile.
3. In the General section, assign a name to your profile.
4. Select the Proxy payload and Enable App Tunnel and set your App Tunnel Mode to the proxy you plan on using.
5. Click Save to create or update your app wrapping profile.
![](./e658225c-f0bd-4b9b-94fb-05138bc40336)

### Logic Implementation

#### AWHttpClient

`AWHttpClient` is a subclass of the org.apache class, `DefaultHttpClient`. It has been repackaged to provide the tunneling and SSO (integrated authentication) features, depending on your business use case.

Implementing the `AWHttpClient` is identical to the way you may implement it’s parent class, `DefaultHttpClient`. You would instantiate a client and an http request, following by executing the client on a specified endpoint URL.

In the provided sample app within the [integration samples repo](https://github.com/euc-releases/workspace-ONE-SDK-integration-samples), you will find an example implementation in the `ProxyActivity.java` class, as shown below. The response body will be logged to the debug console.

```JAVA
package com.airwatch.sdksampleapp;

import android.os.Bundle;
import android.util.Log;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

import com.airwatch.gateway.clients.AWHttpClient;
import com.airwatch.ui.activity.SDKBaseActivity;

import org.apache.commons.io.IOUtils;
import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpGet;

import java.io.InputStream;

public class ProxyActivity extends SDKBaseActivity {

    private static final String TAG = ProxyActivity.class.getSimpleName();

    private Button mConnect = null;
    private String mLoadUrl = "https://air-watch.com";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_proxy);

        mConnect = (Button) findViewById(R.id.connect);
        mConnect.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(getApplicationContext(),
                                "Connecting to " + mLoadUrl, Toast.LENGTH_LONG).show();
                startHttpThread();
            }
        });
    }

    private void startHttpThread(){
        new Thread(new Runnable() {
            @Override
            public void run() {
                AWHttpClient client = new AWHttpClient(getApplicationContext());

                HttpGet request = new HttpGet(mLoadUrl);
                HttpResponse response = null;
                try {
                    response = client.execute(request);
                    if (response != null) {
                        InputStream in = response.getEntity().getContent();
                        String body = IOUtils.toString(in, "UTF-8");
                    } else {
                        Log.e(TAG, "response === null");
                    }
                } catch (Exception e) {
                    Log.e(TAG, "Error : " + e);
                    e.printStackTrace();
                }
            }
        }).start();
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.menu_proxy, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        int id = item.getItemId();
        if (id == R.id.action_settings) {
            return true;
        }
        return super.onOptionsItemSelected(item);
    }
}
```

#### AWWebView and AWWebViewClient

Like their sister, `AWHttpClient`, `AWWebView` and `AWWebViewClient` are subclasses of `WebView` and `WebViewClient`, respectively. Also like their sibling, they can be used in much the same way as their parent classes.

##### Set up the AWWebView and AWWebViewClient

The approach taken in the sample app was to create an `AWWebView` class, in order to include the url loading logic and set it’s `WebViewClient`.

You will find the subclass of `AWWebView` in a class named `TestWebView.java` in the sample app within the [integration samples repo](https://github.com/euc-releases/workspace-ONE-SDK-integration-samples) for this module. You can set up the UI by having the following View object in the layout xml:

```XML
<com.airwatch.sdksampleapp.TestWebView
    android:id="@+id/awwebview"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:layout_below="@+id/input">
</com.airwatch.sdksampleapp.TestWebView>
```

Here you can find TestWebView.java:

```JAVA
package com.airwatch.sdksampleapp;

import android.content.Context;
import android.util.AttributeSet;
import android.webkit.WebView;

import com.airwatch.auth.napps.NappsConstants;
import com.airwatch.gateway.clients.AWWebView;
import com.airwatch.gateway.clients.AWWebViewClient;
import com.airwatch.proxy.TokenGenerator;
import com.airwatch.proxy.TokenUtility;

import java.util.HashMap;
import java.util.Map;

public class TestWebView extends AWWebView {

    public static final String USER_SUFFIX = " AirWatch Browser";
    private Context mContext;
    private AWWebViewClient mAWWebViewClient;

    public TestWebView(Context context) {
        super(context);
        mContext = context;
        init();
    }

    public TestWebView(Context context, AttributeSet arg1) {
        super(context, arg1);
        mContext = context;
        init();
    }

    public TestWebView(Context context, AttributeSet arg1, int arg2) {
        super(context, arg1, arg2);
        mContext = context;
        init();
    }

    private void init() {
        mAWWebViewClient =new AWWebViewClient(mContext) {
            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                if (url.contains(NappsConstants.REDIRECT_URL)) {
                    super.shouldOverrideUrlLoading(view,url);
                    return true;
                }
                view.loadUrl(url, mHeaderMap);
                return true;
            }

        };
        mAWWebViewClient.setUserAgentSuffix(USER_SUFFIX);
        getSettings().setJavaScriptEnabled(true);
        setWebViewClient(mAWWebViewClient);
    }

    public void callHttpAuthHandler(String url){
        if(mAWWebViewClient != null){
            mAWWebViewClient.onReceivedHttpAuthRequest(this,null,url,null);
        }
    }

    public static final String REQUEST_TOKEN_HEADER = "X-RT";
    private static Map<String, String> mHeaderMap = new HashMap<String, String>();

    @Override
    public void loadUrl(String url) {
        int requestToken = TokenGenerator.getCurrentToken();
        String newUserAgent = TokenUtility.appendProxyAuthToken(getSettings().getUserAgentString
                (), USER_SUFFIX);
        getSettings().setUserAgentString(newUserAgent);

        mHeaderMap.put(REQUEST_TOKEN_HEADER, Integer.toString(requestToken));
        setUserAgentSuffix(USER_SUFFIX);
        super.loadUrl(url);
    }
}
```

#### Implement the AWWebView

The `TestWebView` object is then used within the `ProxyActivityAWWebView.java` class to navigate to a user-inputted url, or http://google.com.

```JAVA
package com.airwatch.sdksampleapp;

import android.app.ProgressDialog;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import com.airwatch.gateway.GatewayException;
import com.airwatch.gateway.GatewayManager;
import com.airwatch.gateway.GatewayStatusCodes;
import com.airwatch.gateway.IGatewayStatusListener;
import com.airwatch.gateway.clients.AWWebViewClient;
import com.airwatch.sdk.SDKBaseContextService;
import com.airwatch.sdk.configuration.SDKConfigurationKeys;
import com.airwatch.sdk.context.SDKContextManager;
import com.airwatch.util.Logger;
import com.aw.repackage.org.apache.http.util.TextUtils;

import java.util.concurrent.atomic.AtomicBoolean;

public class ProxyActivityAWWebView extends AppCompatActivity {

    public static final String TAG = ProxyActivityAWWebView.class.getSimpleName();


    private Button mGoBtn;
    private TestWebView webView;
    private ProgressDialog progressDialog;
    private EditText input;
    private GatewayManager mGatewayManager;
    private ProxyListener mProxyListener = new ProxyListener();
    private AtomicBoolean fetchingInProgress  = new AtomicBoolean(false);


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_proxy_activity_awweb_view);

        mGoBtn = (Button) findViewById(R.id.go_btn);
        mGoBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (!TextUtils.isEmpty(input.getText()))
                    loadContent();
            }
        });
        webView = (TestWebView) findViewById(R.id.awwebview);
        input = (EditText) findViewById(R.id.input_password);

        webView.getSettings().setJavaScriptEnabled(true);
        webView.setWebViewClient(new AWWebViewClient(this));

        if (isTunnellingEnabled()) {
            handleProxySetup();
        }
    }

    private boolean isTunnellingEnabled(){
        return Boolean.parseBoolean(SDKContextManager.getSDKContext().getSDKConfiguration()
                .getValue(SDKConfigurationKeys.TYPE_APP_TUNNELING,
                        SDKConfigurationKeys.ENABLE_APP_TUNNEL));
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (isTunnellingEnabled() && mGatewayManager != null) {
            try {
                mGatewayManager.unregisterGatewayStatusListener(mProxyListener);
                Logger.w(TAG, " un register listener");
            } catch (GatewayException e) {
                e.printStackTrace();
            }
        }
    }

    private void showProgress(String message){
        if (progressDialog == null){
            progressDialog = new ProgressDialog(this);
        }
        progressDialog.setMessage(message);
        progressDialog.show();
    }

    private void hideProgress(){
        if (progressDialog != null){
            progressDialog.dismiss();
        }
    }

    private void handleProxySetup(){
        try {
            mGatewayManager = GatewayManager.getInstance(getApplicationContext());
            mGatewayManager.registerGatewayStatusListener(mProxyListener);
            Logger.w(TAG, " register listener");
            if (!mGatewayManager.isRunning()){
                showProgress("configuring proxy");
                mGatewayManager.autoConfigureProxy();
            }else {
                Toast.makeText(ProxyActivityAWWebView.this, "already running", Toast.LENGTH_LONG).show();
            }
        } catch (GatewayException e) {
            Log.e(TAG, "Error handling proxy setup: ", e);
        }
    }

    private void loadContent(){
        hideProgress();
        String url = input.getText().toString();
        if (TextUtils.isEmpty(url)){
            Toast.makeText(ProxyActivityAWWebView.this, "Url please" , Toast.LENGTH_LONG).show();
            return;
        }
        if (!(url.startsWith("http://") || url.startsWith("https://"))){
            url = "http://" + url;
        }
        Log.i(TAG, "loading " + url);
        webView.loadUrl(url);
    }

    public class ProxyListener implements IGatewayStatusListener {

        @Override
        public void onError(final int magErrorCode) {
            Logger.d(TAG, "proxy onError called " + magErrorCode);
            if (GatewayStatusCodes.INVALID_THUMBPRINT == magErrorCode && !fetchingInProgress.getAndSet(true)) {
                ProxyActivityAWWebView.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        webView.stopLoading();
                        Toast.makeText(ProxyActivityAWWebView.this, "proxy error", Toast.LENGTH_LONG).show();
                        Logger.d(TAG, "proxy cert not trusted");
                        showProgress("Re-Fetch Mag Cert");
                        AirWatchSDKContextService.startServiceForMessage(getApplicationContext(),
                                SDKBaseContextService.SDK_FETCH_CERTIFICATE);
                    }
                });
            }
        }

        @Override
        public void onStatusChange(int gatewayStatus) {
            switch (gatewayStatus) {
                case GatewayStatusCodes.STATE_CONFIGURING:
                case GatewayStatusCodes.STATE_ESTABLISHING_CONNECTION:
                    break;
                case GatewayStatusCodes.STATE_STARTED:
                    onProxyStartComplete();
                    break;
                case GatewayStatusCodes.STATE_STOPPED:
                    onProxyStopComplete();
                    break;
                default:
                    hideProgress();
                    Logger.d(TAG, "proxy status code = " + gatewayStatus);
                    break;
            }
        }

        public void onProxyStartComplete() {
            ProxyActivityAWWebView.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    hideProgress();
                    Toast.makeText(ProxyActivityAWWebView.this, "proxy started", Toast.LENGTH_LONG).show();
                    Logger.d(TAG, "proxy onProxyStartComplete called");
                    loadContent();
                }
            });
        }

        public void onProxyStopComplete() {
            ProxyActivityAWWebView.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(ProxyActivityAWWebView.this, "proxy stopped", Toast.LENGTH_LONG).show();
                    Logger.d(TAG, "proxy onProxyStopComplete called");
                }
            });
        }
    }
}
```

Your sample web view should appear like the figure below:
![](./1ef3d6d4-b3e4-40de-94a6-91a45cc11a92)

### Assignment and Deployment

The last step is to assign who should get the app and when.

1. Click Add Assignment.
2. Select or create a smart group with your desired set of device assignments.
3. Configure the push mode and deployment time if applicable.
4. Add the assignment.
5. Once ready, click Save and Publish to start the wrapping and deployment process.
