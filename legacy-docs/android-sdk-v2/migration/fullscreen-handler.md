# Fullscreen Handler

<img src="https://img.shields.io/badge/%20-Android%20v2%20DEPRECATED-FFBA43.svg?logo=android&logoColor=gray">

!!!important
The JW Player SDK for Android v2 is available only to customers with an Enterprise license. JW Player plans to deprecate support for this version of the SDK for Android soon. To ensure that your viewers benefit from ongoing SDK improvements, upgrade to [JW Player SDK for Android v3](https://developer.jwplayer.com/sdk/android/docs/developer-guide/index.html). Please contact your JW Player representative if you have additional questions.
!!!

It is possible to override the default fullscreen behavior. To do this simply implement the `FullscreenHandler` interface or extend the `DefaultFullscreenHandler` class and override any or all of these methods:

| Method                                     | Description                                                                                                                         |
|:-------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------|
| `onFullscreenRequested()`           | Called when the player should enter fullscreen. |
| `onFullscreenExitRequested()` | Called when the player should exit fullscreen.                                    |
| `onResume()`   | Called when the activity containing the JWPlayerView is resumed. You could use this to register Orientation listeners.                                |
| `onPause()`      | Called when the activity containing the JWPlayerView is paused. You could use this to unregister Orientation listeners.               |
| `onDestroy()` | Called when the activity containing the JWPlayerView is destroyed. You could use this to release resources that the FullscreenHandler holds on to. |
| `onAllowRotationChanged(boolean allowRotation)` | Called when the "allow rotation" property of the JWPlayerView has changed, use this to determine whether your FullscreenHandler implementation should listen for device orientation changes. |
| `updateLayoutParams(ViewGroup.LayoutParams layoutParms)` | Called when the layout parameters of the JWPlayerView have been updated. You could use these to restore the player when exiting fullscreen. |
| `setUseFullscreenLayoutFlags(boolean flags)` | Called when JWPlayerView#setUseFullscreenLayoutFlags is called, use this to determine whether you should use the SYSTEM_UI_FLAG_FULLSCREEN and SYSTEM_UI_FLAG_HIDE_NAVIGATION flags in calls to setSystemUiVisibility. |

We also offer an alternative `FullscreenHandler` implementation `MaximizingFullscreenHandler`, if the `DefaultFullscreenHandler` does not fit your use-case you may want to try the MaximizingFullscreenHandler before writing your own implementation.

For more information see the [Javadocs](https://developer.jwplayer.com/sdk/android/reference/).
