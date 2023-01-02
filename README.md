
# Integrate Reklamup with Admob Mediation - ANDROID

## Step 1: Import adapter into your app/game
Add the following implementation dependency with the latest version of the adapter in the app-level  `build.gradle`  file:

repositories {<br /> 
&nbsp;&nbsp;&nbsp;&nbsp;maven {url "https://github.com/reklamupdev/reklamup-admob-adapter/raw/main/maven2" }<br />
}  
  
// ...<br />
dependencies {<br />
&nbsp;&nbsp;&nbsp;&nbsp;implementation fileTree(dir:  'libs', include:  ['*.jar'])<br />
&nbsp;&nbsp;&nbsp;&nbsp;implementation 'com.google.android.gms:play-services-ads:21.4.0'<br />
&nbsp;&nbsp;&nbsp;&nbsp;**implementation 'com.reklamup:admanager-adapter:1.0.3'**<br /> 
}<br />
// ...

**GDPR Compliance**<br />
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
## Step 2: Configure mediation settings for your AdMob ad unit
You need to add Reklamup placements provided by the Reklamup team to the mediation configuration as waterfall ad source for your ad unit.

![enter image description here](https://github.com/reklamuprepo/reklamup-admob-adapter/raw/main/assets/waterfall_ad_source.png)

You can add each placement as **custom event**  as shown in the figure below.

![enter image description here](https://github.com/reklamuprepo/reklamup-admob-adapter/raw/main/assets/custom_event.png)

**Custom Event screen parameters**<br />
**Class Name** : You can use the following parameters depending on the ad unit format of the mediation group.

* Interstitial : com.reklamup.ads.admob.AdmobCustomEventInterstitial
* Rewarded/Rewarded Interstitial : com.reklamup.ads.admob.AdmobCustomEventRewarded
* Banner : com.reklamup.ads.admob.AdmobCustomEventBanner

**Parameter** : Reklamup placement ids for each floor price provided by the reklamup team
