[ws1-client-sdk](../../index.md)/[com.airwatch.sdk](../index.md)/[ICertificateReceiverCallback](index.md)/[onCertificateListReceived](on-certificate-list-received.md)

# onCertificateListReceived

```kotlin
abstract fun onCertificateListReceived(cdl: List<CertificateDefinition>)
```

<div class="api-sig-types" markdown="span">[List](https://developer.android.com/reference/kotlin/java/util/List.html)</div>

Callback invoked when the Anchor App responds to a requestCertificates(String issuerId) request. Implementers should handle the returned certificates as required by the application.

## Parameters

| Name | Description |
|------|-------------|
| cdl | list of CertificateDefinition objects corresponding to the requested issuerId; may be empty if none were found. |
