[ws1-client-sdk](../../index.md)/[com.airwatch.sdk](../index.md)/[SDKManager](index.md)/[deleteCustomAttributes](delete-custom-attributes.md)

# deleteCustomAttributes

```kotlin
open fun deleteCustomAttributes(attributes: List<CustomAttributeData>): Int
```

<div class="api-sig-types" markdown="span">[List](https://developer.android.com/reference/kotlin/java/util/List.html), [CustomAttributeData](../-custom-attribute-data/index.md), [Int](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin-stdlib/kotlin/-int/index.html)</div>

Deletes custom attributes for the given list of attributes. 

 Each [CustomAttributeData](../-custom-attribute-data/index.md) must have group and key fields populated to identify the attributes to delete. 

## Parameters

| Name | Description |
|------|-------------|
| attributes | list of attributes to delete. |

## Return

Positive integer indicating the number of attributes successfully deleted, or SDK_RES_FAIL status code if attributes array is empty/null.

## Throws

| Exception | Condition |
|-----------|-----------|
| [com.airwatch.sdk.AirWatchSDKException](../-air-watch-s-d-k-exception/index.md) | if any attribute is null or has null/empty group or key, if the service returns an error message, if API is not available in Anchor Application, or if binding with Anchor app fails. |
