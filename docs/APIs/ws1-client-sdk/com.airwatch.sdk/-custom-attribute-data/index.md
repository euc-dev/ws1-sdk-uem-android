[ws1-client-sdk](../../index.md)/[com.airwatch.sdk](../index.md)/[CustomAttributeData](index.md)

# CustomAttributeData

```kotlin
open class CustomAttributeData
```

Unified data carrier for custom attribute operations (read, write, delete). 

 Encapsulates a custom attribute's group, key, and optional value. 

- **Read requests:** populate group and key; value is ignored on input and filled by the service in the response.
- **Write requests:** populate group and key; value may be null or empty.
- **Delete requests:** populate group and key; value is ignored.

 The value field is nullable. It is only relevant for write operations and read responses.

## See also

- [com.airwatch.sdk.SDKManager](../-s-d-k-manager/delete-custom-attributes.md)

## Properties

| Name | Summary |
|---|---|
| [group](group.md) | open val [group](group.md): [String](https://developer.android.com/reference/kotlin/java/lang/String.html)<br>The group or category to which the custom attribute belongs. |
| [key](key.md) | open val [key](key.md): [String](https://developer.android.com/reference/kotlin/java/lang/String.html)<br>The unique identifier or name of the custom attribute. |
| [value](value.md) | open val [value](value.md): [String](https://developer.android.com/reference/kotlin/java/lang/String.html)<br>The data value associated with the custom attribute. |
