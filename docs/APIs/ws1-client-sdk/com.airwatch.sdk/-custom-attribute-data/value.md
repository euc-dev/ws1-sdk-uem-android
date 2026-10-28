[ws1-client-sdk](../../index.md)/[com.airwatch.sdk](../index.md)/[CustomAttributeData](index.md)/[value](value.md)

# value

```kotlin
open val value: String
```

<div class="api-sig-types" markdown="span">[String](https://developer.android.com/reference/kotlin/java/lang/String.html)</div>

The data value associated with the custom attribute. Nullable — only meaningful for write operations and read responses. On write, a null value is stored as an empty string. On read, an attribute that has not been set is returned with an empty value.
