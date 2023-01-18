
# Integrate Reklamup with Admob Mediation

Reklamup Android adapter for Admob.

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)

## Features

- [x] Banner
- [x] Interstitial
- [x] Rewarded
- [x] Rewarded Interstitial

## Requirements

- Google Mobile Ads SDK 20.0.0 or higher
- Use Android Studio 3.2 or higher
- A minSdkVersion of 19 or higher
- A compileSdkVersion of 28 or higher

## Installation
### Import adapter into your app/game

Add the following implementation dependency with the latest version of the adapter in the app-level  `build.gradle`  file:

repositories {<br /> 
&nbsp;&nbsp;&nbsp;&nbsp;maven {url "https://github.com/reklamupdev/reklamup-admob-adapter/raw/main/maven2" }<br />
}  
  
// ...<br />
dependencies {<br />
&nbsp;&nbsp;&nbsp;&nbsp;implementation fileTree(dir:  'libs', include:  ['*.jar'])<br />
&nbsp;&nbsp;&nbsp;&nbsp;implementation 'com.google.android.gms:play-services-ads:21.4.0'<br />
&nbsp;&nbsp;&nbsp;&nbsp;**implementation 'com.reklamup:admanager-adapter:1.0.4'**<br /> 
}<br />
// ...

## Usage
### GDPR Compliance<br />
If you are not using any Consent Management Platform to handle privacy issues and managing user consent with your own solution, you have to inform admob mediation and mediation partners about the consent. The following code snippet is sample for gdpr consent usage for admob mediation. If you already have the snippet like below you need to add all these extras bundles for the reklamup custom event adapter as well.
        
```java
AdRequest.Builder builder = new AdRequest.Builder();
Bundle extras = new Bundle();
extras.putString("npa", "1");
builder.addNetworkExtrasBundle(AdMobAdapter.class, extras);

// Add this for Reklamup
builder.addNetworkExtrasBundle(type.equals("banner") ? AdmobCustomEventBanner.class :
                type.equals("rewarded") ? AdmobCustomEventRewarded.class :
                        AdmobCustomEventInterstitial.class,
        extras);

```
### Configure mediation settings for your AdMob ad unit
You need to add Reklamup placements provided by the Reklamup team to the mediation configuration as waterfall ad source for your ad unit.

![enter image description here](https://github.com/reklamupdev/reklamup-admob-adapter/raw/main/assets/waterfall_ad_source.png)

You can add each placement as **custom event**  as shown in the figure below.

![enter image description here](https://github.com/reklamupdev/reklamup-admob-adapter/raw/main/assets/custom_event.png)

**Custom Event screen parameters**<br />
**Class Name** : You can use the following parameters depending on the ad unit format of the mediation group.

* Interstitial : com.reklamup.ads.admob.AdmobCustomEventInterstitial
* Rewarded/Rewarded Interstitial : com.reklamup.ads.admob.AdmobCustomEventRewarded
* Banner : com.reklamup.ads.admob.AdmobCustomEventBanner

**Parameter** : Reklamup placement ids for each floor price provided by the reklamup team

## FAQ

You can send email. [ReklamUP](mailto:dev@reklamup.com?subject=Reklamup%20Admob%20Adapter%20Android)<br/>
Click <a href="https://github.com/reklamupdev/reklamup-admob-adapter.ios">here</a> for IOS documentation.

## Credits

ReklamUP is owned and maintained by the [ReklamUP](http://reklamup.com).

## License

Copyright © 2023. All right reserved.
