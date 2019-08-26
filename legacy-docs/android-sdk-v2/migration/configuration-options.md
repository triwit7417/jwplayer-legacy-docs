# Added Configuration Options

<img src="https://img.shields.io/badge/%20-Android%20v2%20DEPRECATED-FFBA43.svg?logo=android&logoColor=gray">

!!!important
The JW Player SDK for Android v2 is available only to customers with an Enterprise license. JW Player plans to deprecate support for this version of the SDK for Android soon. To ensure that your viewers benefit from ongoing SDK improvements, upgrade to [JW Player SDK for Android v3](https://developer.jwplayer.com/sdk/android/docs/developer-guide/index.html). Please contact your JW Player representative if you have additional questions.
!!!

| XML Attribute                   | Description                                                                                                                                                                                                                                                                                                                                                          |
|:--------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `jw_captions_color`             | Hex color of the captions text. Is ffffff by default.                                                                                                                                                                                                                                                                                                                |
| `jw_captions_fontSize`          | Size of the captions text. Is 15 points by default.                                                                                                                                                                                                                                                                                                                  |
| `jw_captions_fontFamily`        | Family of the captions text. Is sans by default.                                                                                                                                                                                                                                                                                                                     |
| `jw_captions_fontOpacity`       | Alpha value of the captions text. Is 100 by default.                                                                                                                                                                                                                                                                                                                 |
| `jw_captions_backgroundColor`   | Hex color of the caption characters background. Is 000000 by default.                                                                                                                                                                                                                                                                                                |
| `jw_captions_backgroundOpacity` | Alpha value of the caption characters background. Is 75 by default.                                                                                                                                                                                                                                                                                                  |
| `jw_captions_edgeStyle`         | Method by which the captions characters are separated from their background.                                                                                                                                                                                                                                                                                         |
| `jw_captions_windowColor`       | Hex color of the background of the entire captions area. Is 000000 by default.                                                                                                                                                                                                                                                                                       |
| `jw_captions_windowOpacity`     | Alpha value of the background of the entire captions area. Is 0 by default.                                                                                                                                                                                                                                                                                          |
| `jw_logo_file`                  | Location of an external JPG, PNG or GIF image to be used as watermark. We recommend using 24 bit PNG images with transparency, since they blend nicely with the video.                                                                                                                                                              |
| `jw_logo_hide`                  | By default (false), the logo remains visible all the time. When this option is set to true, the logo will automatically show and hide along with the other player controls.                                                                                                                                                                                          |
| `jw_logo_link`                  | HTTP URL to jump to when the watermark image is clicked (e.g. http://example.com/). If it is not set, a click on the watermark does nothing in particular.                                                                                                                                                                                                           |
| `jw_logo_margin`                | The distance of the logo from the edges of the display. The default is 8 pixels.                                                                                                                                                                                                                                                                                     |
| `jw_logo_position`              | This sets the corner in which to display the watermark. Uses an enum that can be TOP_RIGHT (the default), TOP_LEFT, BOTTOM_RIGHT or BOTTOM_LEFT. Note the default position is preferred, since the logo won't interfere with the controlbar, captions, overlay ads and dock buttons.
|
| `jw_skin_name`                  | The skin to use for styling the player. If not configured, we'll default our player to use the seven skin. Other available premade skins include six, five, beelden, vapor, roundster, bekle, stormtrooper, and glow. A live example showing each of these, as well as a deeper explanation of custom colors, can be found on our JW Player skin configuration page. |
| `jw_skin_active`                | The color of active skin elements. This should be entered in either hex or x11 color format.                                                                                                                                                                                                                                                                         |
| `jw_skin_inactive`              | The color of inactive skin elements. Like the above active config, this should be entered in either hex or x11 color format.                                                                                                                                                                                                                                         |
| `jw_skin_background`            | The color of a skin's background portion. Like the above active config, this should be entered in either hex or x11 color format.                                                                                                                                                                                                                                    |
| `jw_skin_url`                   | If using an external CSS file to style your player, this can be specified here. Note that with this configuration you will still need to specify the name of your skin and this may negatively impact the speed which your JW Player loads                                                                                                                           |

## Modified Configuration Options

| 1.x            | 2.x            | Description of Changes      |
|:---------------|:---------------|:----------------------------|
| `jw_autoStart` | `jw_autostart` | Start changed to lower case |
| `jw_posterURL` | `jw_image`     | Renamed                     |

## Removed Configuration Options

| XML Attribute              |
|:---------------------------|
| `jw_controlsFullscreen`    |
| `jw_controlsQuality`       |
| `jw_controlsTimePlayed`    |
| `jw_controlsTotalDuration` |
| `jw_controlsSeekEnabled`   |
| `jw_replayButtonEnabled`   |
| `jw_posterDrawable`        |
