# Advertising

<img src="https://img.shields.io/badge/%20-Android%20v2%20DEPRECATED-FFBA43.svg?logo=android&logoColor=gray">

!!!important
The JW Player SDK for Android v2 is available only to customers with an Enterprise license. JW Player plans to deprecate support for this version of the SDK for Android soon. To ensure that your viewers benefit from ongoing SDK improvements, upgrade to [JW Player SDK for Android v3](https://developer.jwplayer.com/sdk/android/docs/developer-guide/index.html). Please contact your JW Player representative if you have additional questions.
!!!

The JW Player supports two different advertising systems, advertising through regular `VAST` tags and advertising through Google Interactive Media Ads (IMA).

## VAST Advertising

### Playing a VAST Ad

In order to play a `VAST` ad, you have to create a `PlaylistItem` that contains an `AdSchedule` and you have to load that into the JW Player.

**Note:** VAST advertisements must have CORS configured in order to work with the JW Player SDK for Android versions 2.3.0 and greater.  This configuration is described in the VAST specification on page 16: [http://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf](http://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

Example:

```java
// Construct a new Ad
Ad ad = new Ad(AdSource.VAST, "http://url-to-vast-tag.xml");

// Construct a new linear AdBreak containing the Ad
// This AdBreak will play a midroll at 10%
AdBreak adBreak = new AdBreak("10%", ad);

// Create a new AdSchedule containing the AdBreak we just created
LinkedList<AdBreak> schedule = new LinkedList<>();
schedule.add(adBreak);

// Using the PlaylistItem.Builder build a new PlaylistItem containing the schedule.
PlaylistItem item = new PlaylistItem.Builder()
    .file("http://url.with.content/file.mp4")
    .schedule(schedule) // Set the Ad Schedule
    .build();

// Load the playlist item with the AdSchedule into the Player
player.load(item);
```

#### Non-linear Overlay Ads

In addition to standard, linear video advertising, JW Player also supports a method of displaying ad banners as an overlay on video content. This means that advertisements can appear in-line without disrupting playback. This method of advertising is known as a non-linear overlay.

Non-linear ads are configured via VAST in a similar way to linear ads, the only difference is that you have to set the `AdType` property to `NONLINEAR`.

### Playing a VMAP

Besides regular VAST tags, the JW Player also supports VMAP's. Because VMAP's already contain an ad schedule, you don't need to set them yourself anymore.

Currently VMAP's are only supported for an entire playlist. They are supplied to the player through `VMAPAdvertising` objects.

Example:

```java
// Create a new VMAPAdvertising
Advertising advertising = new VMAPAdvertising(AdSource.VAST, "http://path-to-vmap-tag.xml");

// Create a new Playlist
PlaylistItem item = new PlaylistItem.Builder()
    .file("http://url.with.content/file.mp4")
    .build();
LinkedList<PlaylistItem> playlist = new LinkedList<>();
playlist.add(item);

// Load the playlist and the VMAP into the player.
player.load(playlist, advertising);
```

### Playing a VAST Ad for an Entire Playlist

It is also possible to create an `Advertising` object and use that for an entire playlist. The `Advertising` will then be applied to every item in the Playlist.

Example:

```java
// Construct a new Ad
Ad ad = new Ad(AdSource.VAST, "http://url-to-vast-tag.xml");

// Construct a new AdBreak containing the Ad
// This AdBreak will play a midroll at 10%
AdBreak adBreak = new AdBreak("10%", ad);

// Create a new AdSchedule containing the AdBreak we just created
LinkedList<AdBreak> schedule = new LinkedList<>();
schedule.add(adBreak);

// Create a new Advertising that contains the AdSchedule
Advertising advertising = new Advertising(AdSource.VAST, schedule);

// Create a new Playlist
PlaylistItem item = new PlaylistItem.Builder()
    .file("http://url.with.content/file.mp4")
    .build();
LinkedList<PlaylistItem> playlist = new LinkedList<>();
playlist.add(item);

// Load the playlist with the advertising into the player.
player.load(playlist, advertising);
```

## Google Interactive Media Ads (IMA)

Google IMA supports both `VAST` and `VMAP` advertising.

### Loading a VAST Tag into Google IMA

Using Google IMA with `VAST` tags is very similar to using JW Player's regular VAST advertising API. The creation process is basically the same, except you set the AdSource to `IMA` instead of `VAST`.

Example:

```java
// Construct a new Ad
Ad ad = new Ad(AdSource.IMA, "http://url-to-vast-tag.xml");

// Construct a new AdBreak containing the Ad
// This AdBreak will play a midroll at 10%
AdBreak adBreak = new AdBreak("10%", ad);

// Create a new AdSchedule containing the AdBreak we just created
LinkedList<AdBreak> schedule = new LinkedList<>();
schedule.add(adBreak);

// Using the PlaylistItem.Builder build a new PlaylistItem containing the schedule.
PlaylistItem item = new PlaylistItem.Builder()
    .file("http://url.with.content/file.mp4")
    .schedule(schedule) // Set the Ad Schedule
    .build();

// Load the playlist item with the AdSchedule into the Player
player.load(item);
```

### Loading a VMAP into Google IMA

Loading a VMAP into Google IMA is very similar to loading a "regular" VMAP.

Example:

```java
// Create a new ImaVMAPAdvertising
Advertising advertising = new ImaVMAPAdvertising("http://path-to-vmap-tag.xml");

// Create a new Playlist
PlaylistItem item = new PlaylistItem.Builder()
    .file("http://url.with.content/file.mp4")
    .build();
LinkedList<PlaylistItem> playlist = new LinkedList<>();
playlist.add(item);

// Load the playlist and the VMAP into the player.
player.load(playlist, advertising);
```

## AdBreak Offsets

An AdBreak *offset* describes the point in time at which to play an AdBreak. Values permitted include the words `pre` and `post`, or an offset in seconds:

-	`pre`: specifies that the AdBreak should be played before the video content.
-	`post`: specifies that the AdBreak should be played after the video content.
-	A time value specified in one of the following formats:
	-	Seconds: `50`
	-	Fractional seconds: `50.5`
	-	Percentage of the entire video: `50%`
	-	Timecode (hh:mm:ss.mmm): `01:55:30:000`

## VPAID 2.0 advertisements

As of version 2.3.0 the JW Player SDK for Android supports VPAID 2 creatives.
Using VPAID 2 advertisements with JW Player is easy, however there are a few things to watch out for when using VPAID 2 advertisements.

### Scheduling VPAID 2.0 advertisements

VPAID 2.0 ads are scheduled in the same way as regular VAST advertisements:

```java
Ad ad = new Ad(AdSource.VAST, "http://url-to-vpaid-tag.xml");
AdBreak adBreak = new AdBreak("pre", ad);
LinkedList<AdBreak> schedule = new LinkedList<>();
schedule.add(adBreak);
PlaylistItem item = new PlaylistItem.Builder()
    .file("http://url.with.content/file.mp4")
    .schedule(schedule) // Set the Ad Schedule
    .build();
player.load(item);
```

### VPAID 2.0 support caveats

* Only VPAID 2.0 JavaScript creatives are supported, Flash or Silverlight creatives are not supported.
* HTML5 Fullscreen API's are currently **NOT** supported since the JW Player SDK takes care of it's own fullscreen behavior.
* Because of this you should make sure that your creatives are responsive, they should be able to handle dynamic changes in width and height, which occur for example when a user rotates their device.

We recommend you to test your VPAID creatives within our SDK before distributing them as creatives may throw errors or not work as expected when rendered by the JW Player SDK for Android.

## Advertising Callbacks

### Callbacks

| Callback | Description |
| --- | --- |
| onBeforePlay() | Fired just before the player begins playing. |
| onBeforeComplete() | Fired just before the player completes playing. |
| onAdStarted(String tag, String creativeType) | VPAID-only This API will trigger when a VPAID ad creative signals to our player that it is starting. |
| onAdClick([AdClickEvent](https://developer.jwplayer.com/sdk/android/reference/com/longtailvideo/jwplayer/events/AdClickEvent.html) adClickEvent) | Fired whenever a user clicks an ad to be redirected to its landing page. |
| onAdImpression([AdImpressionEvent](https://developer.jwplayer.com/sdk/android/reference/com/longtailvideo/jwplayer/events/AdImpressionEvent.html) adImpressionEvent) | Fired based on the IAB definition of an ad impression. |
| onAdComplete([AdCompleteEvent](https://developer.jwplayer.com/sdk/android/reference/com/longtailvideo/jwplayer/events/AdCompleteEvent.html) adCompleteEvent) | Fired whenever an ad has completed playback. |
| onAdSkipped([AdSkippedEvent](https://developer.jwplayer.com/sdk/android/reference/com/longtailvideo/jwplayer/events/AdSkippedEvent.html) adSkippedEvent) | Fired whenever an ad has been skipped. |
| onAdRequest([AdRequestEvent](https://developer.jwplayer.com/sdk/android/reference/com/longtailvideo/jwplayer/events/AdRequestEvent.html) adRequestEvent) | Fired whenever an ad is requested by the player. |
| onAdTime([AdTimeEvent](https://developer.jwplayer.com/sdk/android/reference/com/longtailvideo/jwplayer/events/AdTimeEvent.html) adTimeEvent) | Fired while ad playback is in progress. |
| onAdPause([AdPauseEvent](https://developer.jwplayer.com/sdk/android/reference/com/longtailvideo/jwplayer/events/AdPauseEvent.html) adPauseEvent) | Fired whenever an ad is paused. |
| onAdPlay([AdPlayEvent](https://developer.jwplayer.com/sdk/android/reference/com/longtailvideo/jwplayer/events/AdPlayEvent.html) adPlayEvent) | Fired whenever an ad starts playing or when an ad is unpaused. |
| onAdError(String tag, String message) |  Fired whenever an error prevents the ad from playing. Supported for VAST and IMA. |

### Version 2 changes
Some event listeners are being deprecated, instead of using On{EVENT_NAME}Listener use On{EVENT_NAME}ListenerV2

| New Callbacks | Old Callback |
| --- | --- |
| `onAdClick(AdClickEvent adClickEvent)` | `onAdClick(String tag)` |
| `onAdImpression(AdImpressionEvent adImpressionEvent)` | `onAdImpression(String tag, String creativeType, String adPosition)` |
| `onAdComplete(AdCompleteEvent adCompleteEvent)` | `onAdComplete(String tag)` |
| `onAdSkipped(AdSkippedEvent adSkippedEvent)` | `onAdSkipped(String tag)` |
| `onAdRequest(AdRequestEvent adRequestEvent)` | `onAdSkipped(String tag)` |
| `onAdTime(AdTimeEvent adTimeEvent)` | `onAdTime(String tag, long position, long duration, int sequence)` |
| `onAdPause(AdPauseEvent adPauseEvent)` | `onAdPause(String tag, PlayerState oldState)` |
| `onAdPlay(AdPlayEvent adPlayEvent)` | `onAdPlay(String tag, PlayerState oldState)` |
