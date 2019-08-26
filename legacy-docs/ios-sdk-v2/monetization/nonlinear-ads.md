# Non-linear ads

<img src="https://img.shields.io/badge/%20-iOS%20v2%20DEPRECATED-FFBA43.svg?logo=apple">

!!!important
The JW Player SDK for iOS v2 is available only to customers with an Enterprise license. JW Player plans to deprecate support for this version of the SDK for iOS soon. To ensure that your viewers benefit from ongoing SDK improvements, upgrade to [JW Player SDK for iOS v3](https://developer.jwplayer.com/sdk/ios/docs/developer-guide/). Please contact your JW Player representative if you have additional questions.
!!!

Non-linear ads are now supported by our vast plugin. You can either pass in a non-linear ad tag or pass in a VMAP file containing an ad overlay; in the case of a non-linear ad tag, you must set the JWAdBreak nonlinear property to YES.
Please note that Google IMA does not support non-linear ads as of version B15. 


	JWAdBreak *nonlinearAdBreak = [JWAdBreak adBreakWithTag:@"nonlinear/ad.xml" offset:@"5"];
     nonlinearAdBreak.nonlinear = YES;