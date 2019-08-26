# Methods

<img src="https://img.shields.io/badge/%20-Android%20v2%20DEPRECATED-FFBA43.svg?logo=android&logoColor=gray">

!!!important
The JW Player SDK for Android v2 is available only to customers with an Enterprise license. JW Player plans to deprecate support for this version of the SDK for Android soon. To ensure that your viewers benefit from ongoing SDK improvements, upgrade to [JW Player SDK for Android v3](https://developer.jwplayer.com/sdk/android/docs/developer-guide/index.html). Please contact your JW Player representative if you have additional questions.
!!!

## Playback
These methods are used to retrieve and change the current playback state of the Player: is the Player idle, buffering, playing or paused.

**load(JWMediaSource jwMediaSource)**
The load method will load a media from a provided URL. Similar to the view properties, the Load method contains optional poster url and internal drawable to show as poster images. 

Load media from a given JWMediaSource. This JWMediaSource can be a SingleSource if there is just a unique URL, or can be a MultipleQualityMediaSource if there are multiple qualities for a video.

**getState()**
Get the state of the Player (IDLE, BUFFERING, PLAYING, or PAUSED) 

* IDLE: either playback has not started or playback was stopped (due to a stop() call or an error). Either the play or the error icon is visible in the display.
* BUFFERING: user pressed play, but sufficient data to start playback has to be loaded first. The buffering icon is visible in the display.
* PLAYING: the video is currently playing. No icon is visible in the display.
* PAUSED: the video is currently paused. The play icon is visible in the display.

**pause(state)**  
Toggles playback of the Player. If the state is set true the Player will pause, if set false the Player will start playing and if omitted, the Player will toggle playback.

**play(state)**  
Toggles playback of the Player. If the state is set true the Player will start playing, if set false the Player will pause and if omitted, the Player will toggle playback.

**playAd(url)**  
In addition to using a VAST ad schedule (see the “Adding VAST Ads” section below), the SDK supports playing ads on an ad-hoc basis using the playAd() method. Simply specify the URL of the VAST tag and the ad will play immediately.

**stop()**  
Stops the Player (returning it to the IDLE state) and unloads the currently playing media file.

**onPlay(callback)**  
Fired when the Player enters the PLAYING state. Event attributes:
oldstate (String): the state the Player moved from. Can be BUFFERING or PAUSED.

**onPause(callback)**  
Fired when the Player enters the PAUSED state. Event attributes:
oldstate (String): the state the Player moved from. Can be BUFFERING or PLAYING.

**onBuffer(callback)**  
Fired when the Player enters the BUFFERING state. Event attributes:
oldstate (String): the state the Player moved from. Can be IDLE, PLAYING or PAUSED.

**onIdle(callback)**  
Fired when the Player enters the IDLE state. Event attributes:
oldstate (String): the state the Player moved from. Can be BUFFERING, PLAYING or PAUSED.

**onComplete(callback)**  
Fired when an item completes playback. It has no event attributes.

**onError(callback)**  
Fired when a media error has occurred, causing the Player to stop playback and go into IDLE mode. Event attributes:

* message (String): The reason for the error. See section on Error Messages for a list of possible media errors.

## **Seeking**   
These methods are used to retrieve and update the current media playback position.

**getPosition()**  
Get the current playback position (playhead) in milliseconds, or -1 if playback is not active

**getDuration()**  
Get the duration of the current media in milliseconds, or -1 if unknown. Note that the duration is not available until the first frame of the media has played.

**seek(position)**  
Jump to the specified position within the currently playing media. The position is required and must be provided as an integer, in milliseconds.

**onSeek(callback)**  
Fired after a seek has been requested either by scrubbing the controlbar or through the API. Event attributes:

* position (Number): The position of the Player before the Player seeks (in milliseconds).
* offset (Number): The user requested position to seek to (in milliseconds). Note the actual position the Player will eventually seek to may differ, e.g. because HLS can only seek to fragment boundaries.

**onTime(callback)**  
While the Player is playing, this event is fired as the playback position gets updated. This may occur as frequently as 10 times per second. Event attributes:

* duration(Number): Duration of the current item in milliseconds.
* position(Number): Playback position in milliseconds.

## **Controls and Fullscreen**  
The controls of the Player (buttons, etc) should be configured using the layout XML properties of JWPlayerView. See the JWPlayerView description under “Classes and Methods.”

The following methods allow you to use fullscreen features of the Player.

**getFullscreen()**  
Find out whether the Player is currently playing in fullscreen mode. Returns either true or false.

**setFullscreen(boolean state, boolean allowRotation)**  
Switch to fullscreen mode or back to windowed mode. Method parameters are:

* state: Set to true to make the player fullscreen, false to make windowed mode.
* allowRotation: Set to true to allow rotation of the phone to enter/exit fullscreen, false if rotation should be locked or only changed by another call to setFullscreen().

**onFullscreen(callback)**  
Fired when the Player toggles to and from fullscreen. Event attributes:

* state (boolean): true for fullscreen, false for windowed mode
* userRequest (booelan): true if onFullscreen() was caused by the user tapping the fullscreen button, otherwise false.

## **Autostart and Repeat**
The SDK exposes methods for controlling the Autostart and Repeat:

**setAutoStart(boolean)**
If set to true, the player will start media playback automatically.

**setRepeat(boolean)**
If set to true, the player will repeat the media (or playlist) automatically after completion.

**isAutoStart()**  
Returns (true or false) whether or not the player is set to start media playback automatically.  

**isRepeat()**  
Returns (true or false) whether or not the player is set to repeat the media (or playlist) playback.

## **Playlist**

The public methods for Playlist are:

**first()**  
Plays the first item on the playlist
Returns a boolean to indicate whether or not the operation was successful.

**getCurrent()**  
Returns the current mediaSource in the playlist.

**getCurrentIndex()**  
Returns the index of the current media list item that is playing.

**getLastIndex()**  
Returns the index of the last media in the list.

**getSize()**  
Returns the number of items in the playlist.

**isFinished()**  
Returns a boolean indicating whether or not the playlist has finished (i.e., played the last item in the list).

**isFirst()**  
Returns a boolean indicating whether or not the current media is the first in the playlist.

**isLast()**  
Returns a boolean indicating whether or not the current media is the last in the playlist.

**last()**  
Plays the last source on the playlist.
Returns a boolean indicating whether or not the operation was successful.

**next()**  
Plays the next source on the playlist.
Returns a boolean indicating whether or not the operation was successful.

**previous()**  
Plays the previous source on the playlist.
Returns a boolean indicating whether or not the operation was successful.

**skipTo(index)**  
Plays the media at the specified index in the playlist.
index is an integer indicating the index of the video to be played. (Note that the index count starts at zero, not one.)  
Returns a boolean indicating whether or not the operation was successful.


## **Quality**
The SDK exposes the Quality API calls to allow app developers to switch video stream quality manually. This could be in response to changing network conditions, a user action, or other event. Call attributes are the same as with the web-based JW Player. This API is only relevant if multiple quality levels of the video are available (for example, from an HLS master playlist).

**Note:** Quality switching using the Quality API is not the same as automatic adaptive HLS. When you switch streams using the Quality API, the new media stream is loaded and the player seeks to the playhead position. 

**getQualityLevels(List<QualityLevel> levels)**
Returns an array with quality levels from the Player. Each level is an object that contains a label property from the NAME attribute in the HLS playlist.

**getCurrentQuality()**  
Return the index of the current quality level.

**setCurrentQuality(int index)**
The index of the desired quality level to set the Player to playback.

**onQualityLevels(List<QualityLevel> levels)**
Fired when the list of available quality levels is updated. E.g., happens shortly after a playlist item starts playing.

**onQualityChange(int currentQuality)**
Fired when the active quality level is changed. E.g., happens in response to a user clicking the controlbar quality menu or a script calling setCurrentQuality.

**Note:** HLS Playlist Default Stream Variant
The SDK always begins playback using the first stream variant in the HLS playlist. This is in accordance with the Apple recommended guidelines HLS (see [https://developer.apple.com/library/ios/technotes/tn2224/_index.html](https://developer.apple.com/library/ios/technotes/tn2224/_index.html)) and is true whether you are using adaptive HLS in Android 4.x or the JW Player HLS fallback provider. 

If you want to start playback with a variant other than the first variant, use the **setCurrentQuality(int index)** method in the Quality API. Note that this method cannot be called until **onQualityLevels()** method is called.

## **Advertising**

**onAdComplete(callback)**  
Fired whenever an ad has completed playback. Event attributes:
tag (String): The URL to the VAST XML file (ad tag) that is currently playing.

**onAdSkipped(callback)**  
Fired whenever an ad has been skipped. Event attributes:

* **tag** (String): The URL to the VAST XML file (ad tag) that was skipped.

**onAdPlay(callback)**  
Fired whenever an ad starts to be played. Event attributes:

* **tag** (String): The URL to the VAST XML file (ad tag) that was played.

**onAdPause(callback)**  
Fired when the Ad Player enters the PAUSED state. Event attributes:

* **tag** (String): The URL to the VAST XML file (ad tag) that was paused.

**onAdBuffer(callback)**  
Fired when the Ad Player enters the BUFFERING state. Event attributes:
tag (String): The URL to the VAST XML file (ad tag) that was buffered.

**onAdError(callback)**  
Fired whenever an error prevents the ad from playing. Event attributes:

* **tag** (String): The URL to the VAST XML file (ad tag) that had the error.  
* **message** (String): The error message.

The following error messages are possible:  

1. Invalid ad tag (e.g. invalid XML, broken VAST)
2. Ad tag empty (e.g. no ad available after chasing the wrappers)
3. No compatible creatives (e.g. only FLV video in HTML5)
4. Error playing creative (e.g. a 404 on the MP4 video)
5. Error loading ad tag (for all else)
Unsupported wrapped VAST xml

**onAdImpression(callback)**  
Fired whenever an ad starts playing back. At this point, the VAST tag is loaded and the creative selected. Event attributes:

* **tag** (String): The URL of the ad tag that is currently playing.

**onAdTime(callback)**  
Fired while ad playback is in progress. Event attributes:

* **tag** (String): The URL of the ad tag that is currently playing.
* **position** (Number): The current playback position in the ad creative, in milliseconds.
* **duration** (Number): The total duration of the ad creative.

**onAdClick(callback)**  
Fired whenever a user clicks an ad to be redirected to its landing page. Event attributes:

* **tag** (String): The URL of the ad tag that is currently playing.

## **Captions**

The SDK supports adding caption tracks (subtitles) to video sources. At this time we support the following subtitle formats: SRT, WebVTT and TTML.

To add text captions to a video source, create a `Caption` object using the default constructor and set it's properties.

```
Caption englishCaptions = new Caption();
caption.setFile("https://url/to/caption/en-track.vtt");
caption.setLabel("English");
caption.setDefault(true); // In order to set this track as the default caption track
```

After you've instantiated one or more caption tracks you can add it to a `PlaylistItem`:

```
ArrayList<Caption> captionTracks = new ArrayList<>();
captionTracks.add(englishCaptions);
playlistItem.setCaptions(captionTracks);
```

Now you can load the playlistItem into the JWPlayerView and it will display the captions.

## Metadata

The SDK broadcasts media metadata, these broadcasts allow developers to listen for metadata embedded 
in the current playing media file (e.g. dimensions, bitrates).
To receive these broadcasts you must implement the `VideoAdvertising.onMetaListener` interface.
And register the class that implements the interface onto the JWPlayerView.

Example:

1. Create a class that listens for Metadata:

```
public class MetadataListener implements VideoPlayerEvents.OnMetaListener {
	
	private static final String TAG = "MetadataListener";
	
	/**
	 * Fired when new metadata has been broadcasted by the player.
	 *
	 * @param meta the metadata
	 */
	@Override
	public void onMeta(Metadata meta) {
	    // Prints Meta to logcat in JSON form
		Log.i(TAG, meta.toString());	
	}
}
```

2. Register the listener

```
mPlayerView.addOnMetadataListener(MetadataListener);
```

Note: the actual available metadata may differ between streaming standards and actual streams.

