# Signal event reference

## Events handled

The following events are handled by the Signal extension:

### Rules Engine Response Content

This event is used by the Signal extension to queue and send network calls that correspond to the [Sync PII Consequence](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine/rules-engine-consequence-details#sync-pii-consequence) or postback message.

This event is triggered by the Rules Engine when the events and conditions are met.

#### Event details

| **Event Type** | **Event Source** | **Paired** | **Paired Event** |
| :--- | :--- | :--- | :--- |
| com.adobe.eventType.rulesengine | com.adobe.eventSource.responseContent | No | - |

#### Data payload definition

The key-value pairs in this event correspond to postback and sync PII:

| Key | Friendly name | Type | Optional | Description |
| :--- | :--- | :--- | :--- | :--- |
| triggeredconsequence | Description URL | Map | Yes | Triggered Consequence details in the map.    For the detailed description of each rule consequence, see the following pages:  [Postback consequence](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine/rules-engine-consequence-details#postback-consequence) [Sync PII consequence](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine/rules-engine-consequence-details#sync-pii-consequence) [Open URL consequence](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine/rules-engine-consequence-details#open-url-consequence) |

#### Event data example

Postback message

```text
{
    "id"        : "9d40f5665d5bdbe96dcb3a24f4e4fe98d686a602",
    "type"      : "pb",
    "detail"    : {
        "templateurl"   : "https://www.endpoint.com/post/{%urlenc(~sdkver)%}",
        "templatebody"  : "{\"jsonkey\":\"jsonvalue\",\"sdkkey\":\"{%~sdkver%}\"}",
        "contenttype"   : "application/json",
        "timeout"       : 5
    }
}
```

#### Event data example

Open URL Request with a deeplink URL

```text
{
    "id"                : "48181acd22b3edaebc8a447868a7df7ce629920a",
    "type"            : "url",
    "detail"        : {
            "url"    : "myApp://HomePage"
    }
}
```

### Configuration Response Content

This event is dispatched on the Event Hub when a configuration change is processed. If a change occurs, the listener updates the privacy status.

#### Event details

| **Event Type** | **Event Source** | **Paired** | **Paired Event** |
| :--- | :--- | :--- | :--- |
| com.adobe.eventType.configuration | com.adobe.eventSource.responseContent | No | N/A |

#### Data payload definition

The Signal extension reads the global.privacy key from the configuration event.

| Key | Friendly name | Type | Optional | Description |
| :--- | :--- | :--- | :--- | :--- |
| global.privacy | String | String | No | Contains the mobile privacy status settings. |

#### Event data example

For a configuration change event:

```text
{ "global.privacy": "optedin" }
```

## Dispatched events shared states

The Signal extension does not dispatch events and does not share any shared state.

