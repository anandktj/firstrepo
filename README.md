<br />
= MdotM Android SDK Overview =

The MdotM Android SDK enables high volume Android publishers to earn high CPMs via highly engaging display interstitials, video Ads and rewarded video Ads. Banner formats have been deprecated as of version 3.5 along with framed and styled ads.
<br />

* Current MdotM SDK Version: 3.5.1 (July 19, 2015 Release)
* Android Version Support: 2.2+
* Supported formats: Display Interstitials, Video Ads, Rewarded Video Ads
* Supported Setups: Standalone SDK, Google AdMob, Twitter MoPub, Yahoo Flurry, Unity, PhoneGap, ANE
<br />
=Steps to add MdotM Android SDK to your Android application=
Mentioned below are the steps to follow for adding MdotM Android SDK to your Android application and to initialize the SDK

== Step 1: Getting started with MdotM ==

* [http://platform.mdotm.com/page/register/publisher Sign up] on MdotM website.
* [http://platform.mdotm.com/account/sites Create App Key] upon signing up.
* [http://platform.mdotm.com/sdk/MdotM-Android-SDK-3.5.1.jar Download MdotM Android SDK] 

== Step 2: Add MdotM Android SDK to your project ==

* Copy the downloaded MdotM-Android-SDK-3.5.1.jar SDK file into your Eclipse <b>libs</b> folder. Once added, add this file to the build path.
<br />
[[File:AddingSDK.png|center|800px]]
<br />
== Step 3: Modify your Android Manifest ==

* Define the following activities in the <code>AndroidManifest.xml</code> file

 <activity android:name="com.mdotm.android.view.MdotMActivity" android:launchMode="singleTop"/>
 <activity
            android:name="com.mdotm.android.vast.VastInterstitialActivity"
            android:configChanges="keyboardHidden|orientation"
            android:theme="@android:style/Theme.Translucent.NoTitleBar">
 </activity>

You may choose to add other themes like Fullscreen - without status bar as mentioned below:

 android:theme="@android:style/Theme.Translucent.NoTitleBar.Fullscreen"

* Add the following '''mandatory''' permissions to your manifest file.

 <uses-permission android:name="android.permission.INTERNET" />
 <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

Optionally, add the following permissions to get the cache Ads and to identify the network bandwidth for serving Ads accordingly:

 <uses-permission android:name="android.permission.READ_PHONE_STATE" />
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
 <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />

* [http://developer.android.com/google/play-services/setup.html#Setup Download Google Play Services] and use as Library. Your application tag should contain following line

  <meta-data android:name="com.google.android.gms.version" android:value="@integer/google_play_services_version" /> 

* If you compile with API level 18 or above enabling proguard, then add the following line in your proguard file:

  -dontwarn android.webkit.**

== Step 4: Initialize the SDK  ==

* Create an instance of <code>MdotMAdRequest</code>

   MdotMAdRequest request = new MdotMAdRequest();

* Put in your appkey that you set up on the MdotM website

  request.setAppKey("[INSERT_APP_KEY]");
  request.setTestMode("0");

= Displaying Ads =

Use the code below to display your preferred ad format:

== Interstitials and Video Ads ==

* Create an instance of <code>MdotMInterstitial</code> class.

  MdotMInterstitial interstitial = new MdotMInterstitial(activitycontext);

* Implement <code>MdotMAdEventListener</code> listeners:

 public void onReceiveInterstitialAd();
 public void onFailedToReceiveInterstitialAd();
 public void onInterstitialAdClick();
 public void onDismissScreen();
 public void onInterstitialDismiss();
 public void onLeaveApplicationFromInterstitial();
 public void willShowInterstitial();
 public void didShowInterstitial();

* Call <code>loadInterstitial</code> and pass your <code>MdotMAdEventListeners</code> and request object:

 interstitial.loadInterstitial(this, request);

* Once <code>onReceiveInterstitialAd</code> is called,  you must call <code>showInterstitial(<activitycontext>)</code>:

 interstitial.showInterstitial(this);

== Rewarded Video Ads ==

The implementation of Rewarded Video is the same as the above, except that instead of calling <code>loadInterstitial</code>, you call the following:

  interstitial.loadRewardedVideo(this, request, reward);

and implement the following listener:

 public void onRewardedVideoComplete(boolean skipped, String reward);

If the user completes the video, <code>skipped</code> is <code>false</code> and the user should be rewarded.

If the user skips the video, <code>skipped</code> is <code>true</code> and the user should not be rewarded.

The additional <code>reward</code> parameter should be used in applications where multiple kinds of rewards can be offered to the user.  If there is no ambiguity in reward, an empty string can be provided.

= Testing and Troubleshooting =

Following are the test modes to set to test your SDK implementation

* Set your test mode to "1" to get test Ads

 request.setTestMode("1");

* Set your test mode to "video" to get video test Ads

 request.setTestMode("video");

This will ensure 100% fill rate.

* To test your application for lack of fill, set your test mode to "nofill"

 request.setTestMode("nofill");

This will ensure 0% fill rate.

When you are done testing, revert back to:
 
 request.setTestMode("0");

= Sample Application =
Our sample application provide fully working examples of the MdotM Android SDK for displaying Interstitials, Videos and Rewarded Video Ads.

Mentioned below are the steps to access and setup the sample application:

* Download [http://platform.mdotm.com/sdk/MdotM-Standalone-AndroidSDK-SampleApp-3.5.1.tar.gz MdotM Standalone Android Sample Application]
* Import this file to your workspace.
* Set google-play-service.lib as a library project as shown in the screenshot below

[[File:Sampleapp_screenshot_eclipse.png|center|800px]]
<br />

= Advanced Integrations =

See [[MdotM Android SDK Advanced]] integrations for integrations with AdMob, MoPub, Unity, and more.  

=Support=

Email <code>pubs@mdotm.com</code> for assistance - we are happy to help!
