# Added Callbacks

<img src="https://img.shields.io/badge/%20-Android%20v2%20DEPRECATED-FFBA43.svg?logo=android&logoColor=gray">

!!!important
The JW Player SDK for Android v2 is available only to customers with an Enterprise license. JW Player plans to deprecate support for this version of the SDK for Android soon. To ensure that your viewers benefit from ongoing SDK improvements, upgrade to [JW Player SDK for Android v3](https://developer.jwplayer.com/sdk/android/docs/developer-guide/index.html). Please contact your JW Player representative if you have additional questions.
!!!

| Callback                                               | Description                                                              |
|:-------------------------------------------------------|:-------------------------------------------------------------------------|
| `onCaptionsList(List<Caption> tracks)`                 | Fired when captions tracks are available.                                |
| `onSetupError(String message)`                         | Fired when an error occurs during player setup.                          |
| `onPlaylist(List<PlaylistItem> playlist)`              | Fired when a Playlist is loaded into the player.                         |
| `onPlaylistItem(int index, PlaylistItem playlistItem)` | Fired when a PlaylistItem begins playing.                                |
| `onPlaylistComplete()`                                 | Fired when the last item in a playlist finishes playing.                 |
| `onBeforePlay()`                                       | Fired immediately after the user clicks Play but before playback begins. |
| `onBeforeComplete()`                                   | Fired immediately before content finishes playing.                       |

## Modified Callbacks

| 1.x                                                          | 2.x                                                                  | Description of Changes                                                          |
|:-------------------------------------------------------------|:---------------------------------------------------------------------|:--------------------------------------------------------------------------------|
| `onQualityLevels(QualityLevel[] levels)`                     | `onQualityLevels(final List<QualityLevel> levels)`                   | Quality levels changed from array to List.                                      |
| `onQualityChange(QualityLevel currentQuality)`               | `onQualityChange(int currentQuality)`                                | Quality level parameter changed from QualityLevel to index.                     |
| `onAudioTracks(AudioTrackLevel[] tracksLevels)`              | `onAudioTracks(final List<AudioTrack> audioTracks)`                  | Audio tracks changed from array to List.                                        |
| `onAudioTrackChange(AudioTrackLevel currentAudioTrackLevel)` | `onAudioTrackChange(int currentTrack)`                               | Audio track parameter changed from track to index.                              |
| `onSubtitleSelected(Subtitle subtitle)`                      | `onCaptionsChange(int track, List<Caption> captions)`                | Name changed from onSubtitleSelected(), track index added.                      |
| `onTime(int position, int duration)`                         | `onTime(long position, long duration)`                               | Position and duration types changed from int to long.                           |
| `onFullscreen(boolean state, boolean userRequest)`           | `onFullscreen(boolean fullscreen)`                                   | userRequest parameter removed.                                                  |
| `onMeta(Map<String, String> metaMap)`                        | `onMeta(Metadata meta)`                                              | Metadata is now returned using the `Metadata` class.                            |
| `onAdTime(String adTag, int position, int duration)`         | `onAdTime(String tag, long position, long duration, int sequence)`   | Position and duration types changed from int to long. Sequence parameter added. |
| `onAdImpression(String adTag)`                               | `onAdImpression(String tag, String creativeType, String adPosition)` | Added creativeType and adPosition parameters.                                   |
| `onAdClick(String adTag, String url)`                        | `onAdClick(String tag)`                                              | Removed the URL parameter.                                                      |
| `onBuffer()`                                                 | `onBuffer(PlayerState oldState)`                                     | onBuffer now reports the state the player switched from.                        |
| `onIdle()`                                                   | `onIdle(PlayerState oldState)`                                       | onIdle now reports the state the player switched from.                          |
| `onPause()`                                                  | `onPause(PlayerState oldState)`                                      | onPause now reports the state the player switched from.                         |
| `onPlay()`                                                   | `onPlay(PlayerState oldState)`                                       | onPlay now reports the state the player switched from.                          |
| `onAdPlay(String adTag)`                                     | `onAdPlay(String tag, PlayerState oldState)`                         | onAdPlay now reports the state the player switched from.                        |
| `onAdPause(String adTag)`                                    | `onAdPause(String tag, PlayerState oldState)`                        | onAdPause now reports the state the player switched from.                       |

## Removed Callbacks

| Callback                                             | Description                                                          |
|:-----------------------------------------------------|:---------------------------------------------------------------------|
| `onSubtitle(String subtitle)`                        | Display of individual subtitles is no longer reported.               |
| `onAdFullscreen(boolean state, boolean userRequest)` | All fullscreen state changes are now reported through onFullscreen() |
| `onAdMeta(Map<String, String> metaMap)`              | All metadata is now reported through onMeta()                        |
| `onAdBuffer(String adTag)`                           |                                                                      |
| `onAdIdle(String adTag)`                             |                                                                      |
| `onMediaSelected()`                                  |                                                                      |
