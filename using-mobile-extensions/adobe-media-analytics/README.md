# Adobe Media Analytics for Audio and Video

## **Configure Media Analytics Extension in Launch**

1. In Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Media Analytics for Audio and Video** extension, and click **Install**.
3. Provide extension settings \(see [Configure Media Analytics Extension](#configure-media-analytics-extension)\).
4. Click **Save**.
5. Follow the publishing process to update your SDK configuration.

### **Configure Media Analytics Extension**

![Adobe Media Analytics Extension Configuration](../../.gitbook/assets/ext-ma-configuration.png)

#### **Tracking Server**

{% hint style="info" %}
This is different from your Analytics tracking server.
{% endhint %}

Provide the tracking server to which all media tracking data should be sent.

#### **Channel**

Channel name property.

#### **Online Video Provider**

Name of the online platform through which content gets distributed.

#### **Player Name**

Name of the media player in use (e.g., "AVPlayer", "Native Player", "Custom Player").

#### **Application Version**

The version of the media player application/SDK.

#### **Debug Logging**

Enables or disables Media SDK logs.

{% hint style="danger" %}
This should be disabled for your production application.
{% endhint %}

### Add Media Analytics to your app

{% hint style="info" %}
This extension requires the [Adobe Analytics Extension](../adobe-analytics/README.md). You must add the Analytics extension to your Launch property and make sure the extension is correctly configured.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
Add the Media extension to your project using the app's Gradle file.

#### Java

1. Import the Media extension in your application's main activity.

```java
import com.adobe.marketing.mobile.*;
```

{% endtab %}

{% tab title="iOS" %}
Add the library to your project via your Cocoapods `Podfile` by adding `pod 'ACPMedia'`.

#### Objective-C

```objectivec
#import <ACPMedia.h>
```

#### Swift

```swift
import ACPMedia
```

{% endtab %}
{% endtabs %}

### Register Media with Mobile Core

{% tabs %}
{% tab title="Android" %}

#### Java

To register media with Mobile Core, call the `setApplication()` method in `onCreate()`, then call setup methods, as shown in this sample:

```java
public class MobileApp extends Application {

  @Override
  public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);

      try {
          Media.registerExtension();  //Register Media with Mobile Core
          Analytics.registerExtension();
          Identity.registerExtension();
      } catch (Exception e) {

      }
  }
}
```

{% endtab %}

{% tab title="iOS" %}
In your app's `application:didFinishLaunchingWithOptions`, register Analytics with Mobile Core:

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPMedia registerExtension];  //Register Media with Mobile Core
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    return YES;
  }
```

#### Swift

```swift
func application(_ application: UIApplication, 
                 didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    ACPMedia.registerExtension();  //Register Media with Mobile Core
    ACPAnalytics.registerExtension();
    ACPIdentity.registerExtension();
    return true;
}
```

{% endtab %}
{% endtabs %}

## Configuration Keys

To update your SDK configuration programmatically, use the following information to change your Media configuration values. For more information, see [Configuration Methods Reference](../mobile-core/configuration-reference/#update-configuration).

| Key                  | Required | Description                                           |
|----------------------|----------|-------------------------------------------------------|
| `media.trackingServer` |    Yes   | [See Tracking Server](#tracking-server)             |
| `media.channel`        |    No    | [See Channel](#channel)                             |
| `media.ovp`            |    No    | [See Online Video Provider](#online-video-provider) |
| `media.playerName`     |    No    | [See Player Name](#player-name)                     |
| `media.appVersion`     |    No    | [See Application Version](#application-version)     |
| `media.debugLogging`   |    No    | [See Debug Logging](#debug-logging)                 |
