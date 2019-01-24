# Interacting with rules

Rules are defined in the Launch interface and can include `data elements`, `events`, `conditions` and `actions` provided by extensions.

## Publishing rules support for Launch

Your extension should publish the rules support it provides to Launch. This is done via the `extension.json` file in your extensions base directory.

### Publishing supported data elements

Data elements can be supported by publishing the shared state keys that you want to use in a rule. For more information, see [Type Definition](https://developer.adobelaunch.com/guides/extensions/extension-manifest/#type-definition).

```text
  "dataElements": [
    {
      "displayName": "My Custom Value",
      "name": "customValue",
      "schema": {
        "$schema": "http://json-schema.org/draft-04/schema#",
        "type": "object",
        "allOf": [{
          "$ref": "https://assets.adobedtm.com/activation/reactor/schemas/1.0/extension-definitions-mobile.json#/definitions/dataElement"
        }]
      },
    },
```

### Publishing supported conditions

Conditions can be supported by publishing the shared state keys or events that you want to use in a rule. For more information, see [Type Definition](https://developer.adobelaunch.com/guides/extensions/extension-manifest/#type-definition).  

Here is an example:

```text
    "events":[
    {
      "displayName": "My Custom Event",
      "name": "triggerEvent",
      "schema": {
        "$schema": "http://json-schema.org/draft-04/schema#",
        "type": "object",
        "allOf": [{
          "$ref": "https://assets.adobedtm.com/activation/reactor/schemas/1.0/extension-definitions-mobile.json#/definitions/events"
        }]
      }
    }],
    "conditions":[
    {
      "displayName": "My Custom Condition",
      "name": "triggerCondition",
      "schema": {
        "$schema": "http://json-schema.org/draft-04/schema#",
        "type": "object",
        "allOf": [{
          "$ref": "https://assets.adobedtm.com/activation/reactor/schemas/1.0/extension-definitions-mobile.json#/definitions/conditions"
        }]
      }
    }],
```

### Publishing supported actions

Conditions can be supported by publishing the events that you want to use in a rule. For more information, see [Type Definition](https://developer.adobelaunch.com/guides/extensions/extension-manifest/#type-definition).  

Here is an example:

```text
    "actions": [
    {
      "displayName": "My Custom Action",
      "name": "com.myCompany.eventType.doSomeWork",
      "schema": {
        "$schema": "http://json-schema.org/draft-04/schema#",
        "type": "object",
        "properties": {},
        "allOf": [{
          "$ref": "https://assets.adobedtm.com/activation/reactor/schemas/1.0/extension-definitions-mobile.json#/definitions/consequence"
        }]
      },
    }],
```

## Supporting rules at runtime

You should provide support for the events, actions, and conditions that you published to Launch at runtime.

### Publishing a shared state `condition` at runtime

A shared state that was published by your extension can be used as a `condition` when configuring a rule in Launch. To learn how you can publish a shared state, see [Updating the Shared State](https://aep-sdks.gitbook.io/docs/resources/building-mobile-extensions/updating-the-shared-state).

### Dispatching an event `condition` at runtime

An event that was dispatched by your extension can be used as a `condition` when configuring a rule in Launch. To learn how you can dispatch an event, see [Dispatching Events from your Extension](https://aep-sdks.gitbook.io/docs/resources/building-mobile-extensions/dispatching-events-from-your-extension).

### Handling an event `action` at runtime

For an event that your extension registered, a listener for can be used as an `action` when configuring a rule in Launch. To learn how you can register a listener for your events, see [Listening for Events](https://aep-sdks.gitbook.io/docs/resources/building-mobile-extensions/event-listeners).

