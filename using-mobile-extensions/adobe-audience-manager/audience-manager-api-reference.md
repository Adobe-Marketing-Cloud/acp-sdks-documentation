# Audience Manager API reference

## Send Signals to Audience Manager

Use this method to send a signal with traits to Audience Manager and get the matching segments returned in a block callback. Audience manager sends the UUID in response to initial signal call.  The UUID is persisted on local SDK storage and is sent by the SDK to Audience Manager in all subsequent signal requests.

If you are using the Experience Cloud ID \(ECID\) Service, the ECID and other custom identifiers for the same visitor are sent with each signal request. The visitor profile returned by Audience Manager is saved in SDK local storage and updated with subsequent signal calls.

{% hint style="info" %}
For more information on UUID and other Audience Manager identifiers, see [Index of IDs in Audience Manager](https://marketing.adobe.com/resources/help/en_US/aam/ids-in-aam.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### **signalWithData**

On Android, the UUID is persisted in `SharedPreferences`.

#### **Syntax**

```java
public static void signalWithData(final Map<String, String> data, final AdobeCallback<Map<String, String>> callback)
```

#### **Example**

```java
AdobeCallback<Map<String, String>> visitorProfileCallback = new AdobeCallback<Map<String, String>>() {
    @Override
    public void call(final Map<String, String> visitorProfile) {
        // your own customized code
    }
};
​
Map<String, String> traits = new HashMap<String, String>();
traits.put("trait", "xyz");
Audience.signalWithData(traits, visitorProfileCallback);
```
{% endtab %}

{% tab title="iOS" %}
### signalWithData

On iOS, UUID is persisted in `NSUserDefaults`.

#### **Syntax**

```java
+ (void) signalWithData: (NSDictionary<NSString*, NSString*>* __nullable) data
                       callback: (nullable void (^) (NSDictionary* __nullable visitorProfile)) callback;
```

#### **Examples** 

**Objective-C**

```objectivec
// objective-c
NSDictionary *traits = @{@"key1":@"value1",@"key2":@"value2"};
[ACPAudience signalWithData:traits callback:^(NSDictionary* visitorProfile){
  // your customized code
}];

```

**Swift**

```swift
// swift
ACPAudience.signal(withData: ["key1": "value1", "key2": "value2"], callback: {(_ response: [AnyHashable: Any]?) -> Void in
  // your customized code
})
```
{% endtab %}
{% endtabs %}

## Reset Identifiers and Profiles

This API helps you reset the Audience Manager UUID and purges the current visitor profile.

{% hint style="info" %}
For more information on UUID, DPID, DPUUID and other Audience Manager identifiers, see [Index of IDs in Audience Manager](https://marketing.adobe.com/resources/help/en_US/aam/ids-in-aam.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### **reset**

#### **Syntax**

```java
public static void reset()
```

#### **Example**

```java
Audience.reset();
```
{% endtab %}

{% tab title="iOS" %}
### **reset**

#### **Syntax**

```objectivec
+ (void) reset;
```

#### **Examples**

**Objective-C**

```objectivec
// objective-c
[ACPAudience reset];
```

**Swift**

```swift
// swift
ACPAudience.reset()
```
{% endtab %}
{% endtabs %}

## Get visitor profile

Returns the visitor profile that was most recently updated. The visitor profile is saved in SDK local storage for access across multiple launches of your app. If no prior audience signal has been sent, a null value is returned when this API is called.

{% tabs %}
{% tab title="Android" %}
### getVisitorProfile

On Android, the visitor profile is saved in `SharedPreferences`.

#### **Syntax**

```java
public static void getVisitorProfile(final AdobeCallback<Map<String, String>> adobeCallback)
```

#### **Example**

```java
AdobeCallback<Map<String, String>> visitorProfileCallback = new AdobeCallback<Map<String, String>>() {
    @Override
    public void call(final Map<String, String> visitorProfile) {
        // your own customized code
    }
};

Audience.getVisitorProfile(visitorProfileCallback);
```
{% endtab %}

{% tab title="iOS" %}
### getVisitorProfile

On iOS, the visitor profile is saved in `NSUserDefaults`.

#### **Syntax**

```java
+ (void) getVisitorProfile: (nonnull void (^) (NSDictionary* __nullable visitorProfile)) callback;
```

#### **Example**

**Objective-C**

```objectivec
// objective-c
[ACPAudience getVisitorProfile:^(NSDictionary* visitorProfile){
  // your customized code
}];
```

**Swift**

```swift
// swift
ACPAudience.getVisitorProfile({(_ response: [AnyHashable: Any]?) -> Void in
    // your customized code
})
```
{% endtab %}
{% endtabs %}

