# Added API Methods

<img src="https://img.shields.io/badge/%20-Android%20v2%20DEPRECATED-FFBA43.svg?logo=android&logoColor=gray">

!!!important
The JW Player SDK for Android v2 is available only to customers with an Enterprise license. JW Player plans to deprecate support for this version of the SDK for Android soon. To ensure that your viewers benefit from ongoing SDK improvements, upgrade to [JW Player SDK for Android v3](https://developer.jwplayer.com/sdk/android/docs/developer-guide/index.html). Please contact your JW Player representative if you have additional questions.
!!!

| Method                                    | Description                                                                         |
|:------------------------------------------|:------------------------------------------------------------------------------------|
| `int getPlaylistIndex()`                  | Returns the index of the currently playing PlaylistItem.                            |
| `PlaylistItem getPlaylistItem(int index)` | Returns the PlaylistItem at the provided index.                                     |
| `List<Caption> getCaptionsList()`         | Returns the list of currently available captions tracks.                            |
| `int getCurrentCaptions()`                | Returns the index of the currently selected captions track.                         |
| `setCurrentCaptions(int index)`           | Sets which captions track to display.                                               |
| `setSkin(Skin skin)`                      | Sets the player skin from the stock set of skins.                                   |
| `setSkin(String skinUrl)`                 | Sets the player skin to the provided URL.                                           |
| `onDestroy()`                             | Called from Activity.onDestroy() or Fragment.onDestroy(), handles resource cleanup. |

## Modified API Methods

### Setup Related Methods

Setup is primarly used to change the player configuration programmatically. It is also possible to update the playlist and advertising settings alongside other configuration changes.

In order to get the current player configuration simply call:

`getConfig()` - which will return the current configuration. Modify the configuration as you see fit and then load it into the player using `setup()`

### Load Related Methods

If you would only like to change the playlist and advertising options without affecting any other settings use the `load()` methods, they are as follows:

| Method                                                       | Description                                                                             |
|:-------------------------------------------------------------|:----------------------------------------------------------------------------------------|
| `load(List<PlaylistItem> playlist, Advertising advertising)` | Used to load a playlist along with advertising options and an ad schedule.              |
| `load(List<PlaylistItem> playlist)`                          | Used to load a playlist, note that each playlist item can have an advertising schedule. |
| `load(PlaylistItem playlistItem)`                            | Used to load a single playlist item.                                                    |

### Return Types for Getters

| Method                                         | Description                                            |
|:-----------------------------------------------|:-------------------------------------------------------|
| `public List<QualityLevel> getQualityLevels()` | Switched to List from array.                           |
| `public List<PlaylistItem> getPlayList()`      | Removed Playlist object in favor of List<PlaylistItem> |
| `List<AudioTrack> getAudioTracks()`            | Switched to List from array.                           |
| `long getPosition()`                           | getPosition now returns a long instead of an int.      |
| `long getDuration()`                           | getDuration now returns a long instead of an int.      |

### Renamed Methods

| Method                                      | Description                                          |
|:--------------------------------------------|:-----------------------------------------------------|
| `public void setControls(boolean controls)` | Method name changed from `setControlBarVisibility()` |

### Method Signature Changes

| Method                    | Description                                                                                     |
|:--------------------------|:------------------------------------------------------------------------------------------------|
| `playAd(String... vasts)` | playAd() can now take multiple ad tags, if one ad tag fails to load the next will be attempted. |

Removed API Methods
-------------------

| Method                                                                | Description                                                            |
|:----------------------------------------------------------------------|:-----------------------------------------------------------------------|
| `setEnableSetSystemUiVisibility(boolean enableSetSystemUiVisibility)` | Replaced with extending FullscreenHandler and setFullscreenHandler().  |
| `boolean isAutoStart()`                                               | AutoStart is now controlled at the Playlist level.                     |
| `setAutoStart(boolean autoStart)`                                     | AutoStart is now controlled at the Playlist level.                     |
| `boolean isRepeat()`                                                  | AutoRepeat is not controlled at the Playlist level.                    |
| `setRepeat(boolean repeat)`                                           | AutoRepeat is not controlled at the Playlist level.                    |
| `release()`                                                           | No longer necessary, use `onPause()`, `onResume()`, and, `onDestroy()` |

## Changes to Media Classes

The names of some media classes have changed and some of their structures have been altered. The new names are:

| 1.x                                             | 2.x                                                                                                                                                                                       | Description of Changes                                                                                                                                             |
|:------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                 | `PlayerConfig`                                                                                                                                                                            | This is a new class, it represents a player configuration and can include: controlbar, caption styling, logo, skin, and advertising settings.                      |
| `SingleSource` and `MultipleQualityMediaSource` | `PlaylistItem`                                                                                                                                                                            | This is the root class for a single piece of media in JW Player. It can contain URLs to captions tracks, media sources, and an ad schedule for this playlist item. |
|                                                 | `MediaSource`                                                                                                                                                                             | Used for multiple-source media, any number of these can be assigned to a single `PlaylistItem`                                                                     |
| `Subtitle`                                      | `Caption`                                                                                                                                                                                 | Represents a caption track, any number of these can be assigned to a single `PlaylistItem`                                                                         |
| `AdBreak`                                       | `AdBreak`                                                                                                                                                                                 | Represents an advertising break, contains a playback offset (pre, post, static midroll, or midroll %) and an `Ad`.                                                 |
|                                                 | `Ad`                                                                                                                                                                                      | Has an `AdSource` of either VAST or IMA and contains any number of tags. Multiple tags are waterfalled - if one fails the next is attempted.                       |
| `Advertising`                                   | `Advertising` or `VMAPAdvertising` these classes contain advertising-related settings (e.g. skip message) and can contain an advertising schedule that is applied to the entire playlist. |                                                                                                                                                                    |

## Builders

It is now possible to instantiate `JWPlayerView` and other Media Classes via a builder. Builders cover all of the configuration options that are possible for a class. And in case of the `JWPlayerView` the builder also supports all the possible XML attributes.

Example:

```java
PlayerConfig playerConfig = new PlayerConfig.Builder()
	.logoFile("jw_logo.png")
	.logoLink("http://jwplayer.com")
	.autostart(true)
	.repeat(true)
	.build();
JWPlayerView p = new JWPlayerView(this, playerConfig);
```

Will create a JW Player instance with a clickable logo, and autostart and autorepeat enabled.

There are also builders for the `Caption`, `MediaSource`, and `PlaylistItem` classes.
