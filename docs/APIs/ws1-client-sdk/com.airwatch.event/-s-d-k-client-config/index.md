[ws1-client-sdk](../../index.md)/[com.airwatch.event](../index.md)/[SDKClientConfig](index.md)

# SDKClientConfig

```kotlin
fun interface SDKClientConfig
```

This to be implemented with the app's Application class and to provide [WS1AnchorEvents](../-w-s1-anchor-events/index.md) object.

## Functions

| Name | Summary |
|---|---|
| [getEventHandler](get-event-handler.md) | abstract fun [getEventHandler](get-event-handler.md)(): [WS1AnchorEvents](../-w-s1-anchor-events/index.md)<br>Apps to handle Anchor app events needs to override this method and return the [WS1AnchorEvents](../-w-s1-anchor-events/index.md). |
