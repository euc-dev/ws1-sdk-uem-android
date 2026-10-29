[ws1-client-sdk](../../index.md)/[com.airwatch.sdk](../index.md)/[SDKManager](index.md)/[readCustomAttributes](read-custom-attributes.md)

# readCustomAttributes

```kotlin
open fun readCustomAttributes(queries: List<CustomAttributeData>): List<CustomAttributeData>
```

<div class="api-sig-types" markdown="span">[List](https://developer.android.com/reference/kotlin/java/util/List.html), [CustomAttributeData](../-custom-attribute-data/index.md)</div>

Reads custom attributes for the given list of queries. 

 Each [CustomAttributeData](../-custom-attribute-data/index.md) specifies a group and key to look up. The returned list contains [CustomAttributeData](../-custom-attribute-data/index.md) objects with the value field populated for each matched query. 

## Parameters

| Name | Description |
|------|-------------|
| queries | list of attribute queries to read. |

## Return

Non-null list of [CustomAttributeData](../-custom-attribute-data/index.md) with values populated, or an empty list if no results are found or if queries is null/empty.

## Throws

| Exception | Condition |
|-----------|-----------|
| [com.airwatch.sdk.AirWatchSDKException](../-air-watch-s-d-k-exception/index.md) | if any query is null or has null/empty group or key, if the service returns an error message, if API is not available in Anchor Application, or if binding with Anchor app fails. |
