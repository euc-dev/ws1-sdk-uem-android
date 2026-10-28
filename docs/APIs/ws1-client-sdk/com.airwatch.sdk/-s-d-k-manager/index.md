[ws1-client-sdk](../../index.md)/[com.airwatch.sdk](../index.md)/[SDKManager](index.md)

# SDKManager

```kotlin
class SDKManager
```

Wrapper class to wrap the communication with the WS1 Anchor Application (Agent or Container). 

 SDK controls access to methods based upton type of application. Apps without permission trying to access methods will throw [AirWatchSDKException](../-air-watch-s-d-k-exception/index.md) Methods have multiple access control Levels as in below: 

- NONE: no restrictions applied
- AW_ONLY: apps signed by WS1 only allowed
- AW_WHITELISTED: apps with signatures white listed by WS1
- AW_MANAGED: apps downloaded and installed by WS1 Anchor Application (Agent or Container) AKA managed apps

 SDK Initialization should be done before accessing information from anchor application. Below is sample usage of this class, showing initialization and fetching custom settings. 

Note: Initialization should be done in a background thread.

```java
try {
  SDKManager sdkManager = SDKManager.init(context);
  String customSettings = sdkManager.getCustomSettings();
} catch (Exception e) {
	 e.printStackTrace();
}
```

## See also

- [com.airwatch.sdk.AirWatchSDKException](../-air-watch-s-d-k-exception/index.md)

## Functions

| Name | Summary |
|---|---|
| [acceptCheckoutEULA](accept-checkout-e-u-l-a.md) | open fun [acceptCheckoutEULA](accept-checkout-e-u-l-a.md)(eulaContentId: [String](https://developer.android.com/reference/kotlin/java/lang/String.html), accepted: [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)): [CheckoutResponse](../../com.airwatch.sdk.shareddevice/-checkout-response/index.md)<br>Request console to check out the device for corresponding user with Accept EULA acknowledgment. |
| [authenticateUser](authenticate-user.md) | open fun [authenticateUser](authenticate-user.md)(userName: [String](https://developer.android.com/reference/kotlin/java/lang/String.html), userPassword: [String](https://developer.android.com/reference/kotlin/java/lang/String.html)): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>Verifies authentication credentials with the console. |
| [autoEnroll](auto-enroll.md) | open fun [autoEnroll](auto-enroll.md)(server: [String](https://developer.android.com/reference/kotlin/java/lang/String.html), groupId: [String](https://developer.android.com/reference/kotlin/java/lang/String.html), user: [String](https://developer.android.com/reference/kotlin/java/lang/String.html), password: [String](https://developer.android.com/reference/kotlin/java/lang/String.html)): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>Enrolls the application silently if agent is not yet enrolled. |
| [autoUnenroll](auto-unenroll.md) | open fun [autoUnenroll](auto-unenroll.md)(): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>UnEnrolls the application silently if agent is enrolled. |
| [checkInDevice](check-in-device.md) | open fun [checkInDevice](check-in-device.md)(): [Int](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-int/index.html)<br>Used to checkin the device. |
| [checkOutDevice](check-out-device.md) | open fun [checkOutDevice](check-out-device.md)(user: [String](https://developer.android.com/reference/kotlin/java/lang/String.html), password: [String](https://developer.android.com/reference/kotlin/java/lang/String.html), groupCode: [String](https://developer.android.com/reference/kotlin/java/lang/String.html)): [CheckoutResponse](../../com.airwatch.sdk.shareddevice/-checkout-response/index.md)<br>Checkouts the device from (login to) a different child organization group than the one it is enrolled to. |
| [deinit](deinit.md) | open fun [deinit](deinit.md)(): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>DeInitializes the WS1 SDK. |
| [deleteCustomAttributes](delete-custom-attributes.md) | open fun [deleteCustomAttributes](delete-custom-attributes.md)(attributes: [List](https://developer.android.com/reference/kotlin/java/util/List.html)&lt;[CustomAttributeData](../-custom-attribute-data/index.md)&gt;): [Int](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-int/index.html)<br>Deletes custom attributes for the given list of attributes. |
| [getAPIVersion](get-a-p-i-version.md) | open fun [getAPIVersion](get-a-p-i-version.md)(): [Int](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-int/index.html)<br>Retrieves the revision level of the WS1 SDK. |
| [getApplicationConfiguration](get-application-configuration.md) | open fun [getApplicationConfiguration](get-application-configuration.md)(): Bundle<br> Fetches key-value pair configuration set for the application in the console. |
| [getApplicationProfile](get-application-profile.md) | open fun [getApplicationProfile](get-application-profile.md)(): ApplicationProfile<br>This method is used to get the Application Profile as defined at the WS1 UEM Console. |
| [getAuthenticationType](get-authentication-type.md) | open fun [getAuthenticationType](get-authentication-type.md)(): [Int](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-int/index.html)<br>Get the Authentication Type set in WS1 UEM Console. |
| [getBindingPackageName](get-binding-package-name.md) | open fun [getBindingPackageName](get-binding-package-name.md)(context: Context): [String](https://developer.android.com/reference/kotlin/java/lang/String.html)<br>Utility method to determine the Anchor App to which SDK will be bound. |
| [getConsoleVersion](get-console-version.md) | open fun [getConsoleVersion](get-console-version.md)(): [Float](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-float/index.html)<br>Provides console version to which device is connected. |
| [getCustomSettings](get-custom-settings.md) | open fun [getCustomSettings](get-custom-settings.md)(): [String](https://developer.android.com/reference/kotlin/java/lang/String.html)<br>Fetches the Custom Settings that are defined for the anchor app i.e., Agent or Workspace. |
| [getDeviceLastCheckinTime](get-device-last-checkin-time.md) | open fun [getDeviceLastCheckinTime](get-device-last-checkin-time.md)(): [Long](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-long/index.html)<br>Get the timestamp (in milliseconds) when the last Beacon was successfully sent. |
| [getDeviceSerialId](get-device-serial-id.md) | open fun [getDeviceSerialId](get-device-serial-id.md)(): [String](https://developer.android.com/reference/kotlin/java/lang/String.html)<br>Returns the device SERIAL ID. |
| [getEnrollmentUsername](get-enrollment-username.md) | open fun [getEnrollmentUsername](get-enrollment-username.md)(): [String](https://developer.android.com/reference/kotlin/java/lang/String.html)<br>Retrieves Enrollment Username assigned to the App which the device is currently enrolled. |
| [getGroupId](get-group-id.md) | open fun [getGroupId](get-group-id.md)(): [String](https://developer.android.com/reference/kotlin/java/lang/String.html)<br>Retrieves the location group in which the device is currently enrolled. |
| [getPasscodePolicy](get-passcode-policy.md) | open fun [getPasscodePolicy](get-passcode-policy.md)(): [PasscodePolicy](../../com.airwatch.sdk.profile/-passcode-policy/index.md)<br>Get the Passcode Policy that is defined on the WS1 UEM Console. |
| [getRestrictionPolicy](get-restriction-policy.md) | open fun [getRestrictionPolicy](get-restriction-policy.md)(): [RestrictionPolicy](../../com.airwatch.sdk.profile/-restriction-policy/index.md)<br>Fetches the Restriction Policy as defined at the WS1 UEM Console. |
| [getSDKProfile](get-s-d-k-profile.md) | open fun [getSDKProfile](get-s-d-k-profile.md)(): IBaseConfiguration<br>Returns the SDK profile manager for the current application. |
| [getSDKProfileJSONString](get-s-d-k-profile-j-s-o-n-string.md) | open fun [getSDKProfileJSONString](get-s-d-k-profile-j-s-o-n-string.md)(): [String](https://developer.android.com/reference/kotlin/java/lang/String.html)<br>Returns the SDK profile as a JSON string from the Anchor app. |
| [getServerName](get-server-name.md) | open fun [getServerName](get-server-name.md)(): [String](https://developer.android.com/reference/kotlin/java/lang/String.html)<br>Retrieves the server name in which the device is currently enrolled. |
| [getServerPort](get-server-port.md) | open fun [getServerPort](get-server-port.md)(): [Int](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-int/index.html)<br>Retrieves the port number in which the device is currently enrolled. |
| [getSharedDeviceStatus](get-shared-device-status.md) | open fun [getSharedDeviceStatus](get-shared-device-status.md)(): [SharedDeviceStatus](../../com.airwatch.sdk.shareddevice/-shared-device-status/index.md)<br>Fetches the SharedDevice status of the current device Access Level = AW_MANAGED (for details on access permission please check [SDKManager](index.md)) |
| [getSSOStatus](get-s-s-o-status.md) | open fun [getSSOStatus](get-s-s-o-status.md)(): [SsoSessionReturnCode](../-sso-session-return-code/index.md)<br>Provides the status of the broker app even before SDKManager instance is initialized. |
| [init](init.md) | open fun [init](init.md)(context: Context): [SDKManager](index.md)<br>Initializes the WS1 SDK. |
| [isCompliant](is-compliant.md) | open fun [isCompliant](is-compliant.md)(): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>Determines if the device is currently in good standings with the compliance rules. |
| [isCompromised](is-compromised.md) | open fun [isCompromised](is-compromised.md)(): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>Determines if the device is rooted as diagnosed by WS1 MDM Agent. |
| [isEnrolled](is-enrolled.md) | open fun [isEnrolled](is-enrolled.md)(): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>Determines if the device is currently enrolled in AirWatch. |
| [isServiceConnected](is-service-connected.md) | open fun [isServiceConnected](is-service-connected.md)(): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>Provides binding status of current app with Anchor app |
| [isSSOEnabled](is-s-s-o-enabled.md) | open fun [isSSOEnabled](is-s-s-o-enabled.md)(): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>Determines if the Single Sign On feature is enabled for the 3rd party application. |
| [isSSOSessionValid](is-s-s-o-session-valid.md) | open fun [isSSOSessionValid](is-s-s-o-session-valid.md)(): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>Provides if SSO session valid. |
| [performSharedDeviceOperation](perform-shared-device-operation.md) | open fun [performSharedDeviceOperation](perform-shared-device-operation.md)(bundle: Bundle, resultReceiver: ResultReceiver)<br>Performs shared device operations such as checkout,checkin etc. |
| [readCustomAttributes](read-custom-attributes.md) | open fun [readCustomAttributes](read-custom-attributes.md)(queries: [List](https://developer.android.com/reference/kotlin/java/util/List.html)&lt;[CustomAttributeData](../-custom-attribute-data/index.md)&gt;): [List](https://developer.android.com/reference/kotlin/java/util/List.html)&lt;[CustomAttributeData](../-custom-attribute-data/index.md)&gt;<br>Reads custom attributes for the given list of queries. |
| [refreshBinding](refresh-binding.md) | open fun [refreshBinding](refresh-binding.md)(context: Context): [SDKManager](index.md)<br>Refreshes the binding of WS1 SDK, when Workspace is installed/removed. |
| [requestCertificates](request-certificates.md) | open fun [requestCertificates](request-certificates.md)(iCrc: [ICertificateReceiverCallback](../-i-certificate-receiver-callback/index.md)): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>Requests the Anchor application to send the Certificates.<br>open fun [requestCertificates](request-certificates.md)(issuerId: [String](https://developer.android.com/reference/kotlin/java/lang/String.html), token: [String](https://developer.android.com/reference/kotlin/java/lang/String.html), iCrc: [ICertificateReceiverCallback](../-i-certificate-receiver-callback/index.md)): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>Requests the Anchor application to send the Certificates corresponding to the requested issuerId. |
| [uploadApplicationLogs](upload-application-logs.md) | open fun [uploadApplicationLogs](upload-application-logs.md)(): [Boolean](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-boolean/index.html)<br>This method is used to upload the application logs to the anchor app. |
| [writeCustomAttributes](write-custom-attributes.md) | open fun [writeCustomAttributes](write-custom-attributes.md)(attributes: [List](https://developer.android.com/reference/kotlin/java/util/List.html)&lt;[CustomAttributeData](../-custom-attribute-data/index.md)&gt;): [Int](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-int/index.html)<br>Writes custom attributes for the given list of attributes. |
