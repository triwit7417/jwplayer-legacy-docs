# Google IMA

<img src="https://img.shields.io/badge/%20-iOS%20v2%20DEPRECATED-FFBA43.svg?logo=apple">

!!!important
The JW Player SDK for iOS v2 is available only to customers with an Enterprise license. JW Player plans to deprecate support for this version of the SDK for iOS soon. To ensure that your viewers benefit from ongoing SDK improvements, upgrade to [JW Player SDK for iOS v3](https://developer.jwplayer.com/sdk/ios/docs/developer-guide/). Please contact your JW Player representative if you have additional questions.
!!!

In order to play ads using Google Interactive Media Ads (Google IMA) you must import the Google IMA framework into your project ( Installing Google IMA ) and set your JWAdConfig’s adClient to googIMA.

    adConfig.adClient = googIMA;

Ads are scheduled for Google IMA the same way they are scheduled using our default ad client (vastPlugin). The VMAP control ad insertion also overrides any adSchedule arrays when using Google IMA. Customization of ad messages and skipping are not handled with Google IMA at the moment, but can be done when creating an ad tag.
The Google IMA ad client can be used in playlists and supports waterfalling, bumpers, as well as standard and optimized ad pods.
