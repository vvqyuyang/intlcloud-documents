## Supported Platforms

Proposed by Google, the WebRTC technology is well supported by Chrome (desktop), Edge (desktop), Firefox (desktop), and Safari (desktop and mobile), but poorly or not supported by other platforms such as browsers on Android.

- If your application scenario is mainly in the education sector, consider using [TRTC SDK for Electron](https://intl.cloud.tencent.com/document/product/647/35097), which supports two-channel big/small video images, with more flexible screen sharing schemes and better recovery capabilities on poor network connections.

<table>
<tr>
<th>OS</th>
<th width="22%">Browser</th><th>Minimum Browser<br>Version Requirement</th><th width="16%">Receive (Playback)</th><th width="16%">Send (Broadcast)</th><th>Screen Sharing</th><th>SDK Version Requirement</th>
</tr><tr>
<td rowspan="4">macOS</td>
<td>Safari (desktop)</td>
<td>11+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Safari 13+)</td>
<td>-</td>
</tr>
<tr>
<td>Chrome (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Chrome 72+)</td>
<td>-</td>
</tr>
<tr>
<td>Firefox (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Firefox 66+）</td>
<td>4.7.0+</td>
</tr>
<tr>
<td>Edge (desktop)</td>
<td>80+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>4.7.0+</td>
</tr>
<tr>
<td  rowspan="4">Windows</td>
<td>Chrome (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Chrome 72+)</td>
<td>-</td>
</tr>
<tr>
<td>QQ browser (desktop, WebKit core)</td>
<td>10.4+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>Firefox (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Firefox 66+）</td>
<td>4.7.0+</td>
</tr>
<tr>
<td>Edge (desktop)</td>
<td>80+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>4.7.0+</td>
</tr>
<tr>
<td>iOS 11.1.2+</td>
<td>Safari (mobile)</td>
<td>11+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>WeChat embedded browser</td>
<td>-</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>WeChat embedded browser</td>
<td>WeChat 6.5+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td  rowspan="4">Android</td>
<td>QQ browser (mobile)</td>
<td>-</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr><tr>
<td>UC browser (mobile)</td>
<td>-</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>WeChat embedded browser (TBS core)</td>
<td>-</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>WeChat embedded browser (XWEB core)</td>
<td>-</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
</table>

## API Guide
The tutorials below offer detailed instructions on how to use different APIs.

| Feature                       | Sample Code                                                                                                      |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Basic audio/video call  | [Tutorial](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-11-basic-video-call.html)               |
| Interactive live streaming | [Tutorial](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-12-basic-live-video.html)                           |
| Switching cameras/mics | [Tutorial](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-13-basic-switch-camera-mic.html)      |
| Setting local video attributes  | [Tutorial](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-14-basic-set-video-profile.html)      |
| Dynamically enabling/disabling local audio/video | [Tutorial](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-15-basic-dynamic-add-video.html) |
| Sharing screen | [Tutorial](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-16-basic-screencast.html)   |
| Detecting volume | [Tutorial](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-17-basic-detect-volume.html) |
| Custom capturing and playback rendering | [Tutorial](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-20-advanced-customized-capture-rendering.html) |
| Specifying the maximum number of upstream users in a room | [Tutorial](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-04-info-uplink-limits.html) |
| Adding music and audio effects | [Tutorial](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-22-advanced-audio-mixer.html)                  |


## TRTC

>!This document applies to 4.x.x versions of TRTC SDK for desktop browsers.

TRTC is the main entry to [TRTC SDK for desktop browsers](https://trtc-1252463788.file.myqcloud.com/web/docs/index.html). You can use TRTC methods to create a client object (`Client`) and local audio/video stream object (`Stream`) for real-time communication, check a browser's compatibility and whether it supports screen sharing, as well as set log levels and upload logs.

| API                                                                                                              | Description                                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VERSION](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.VERSION)                                 | Gets the version number of TRTC SDK for desktop browsers.                                                                                                                                  |
| [checkSystemRequirements](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.checkSystemRequirements) | Checks whether a browser supports TRTC SDK for desktop browsers; if not, ask users to download the latest version of Chrome.                                  |
| [isScreenShareSupported](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.isScreenShareSupported) | Checks whether the browser supports screen sharing. Call this method before creating a screen sharing stream.                                                                  |
| [getDevices](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.getDevices)                           | Returns the list of media input/output devices.                                                                                                                                    |
| [getCameras](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.getCameras)                           | Returns the list of cameras.                                                                                                                                          |
| [getMicrophones](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.getMicrophones)                   | Returns the list of mics.                                                                                                                                          |
| [getSpeakers](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.getSpeakers)                         | Returns the list of speakers.                                                                                                                                          |
| [createClient](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createClient)                       | Creates a client object for real-time audio/video calls. This method needs to be called only once for each call.                                                                                              |
| [createStream](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createStream) | Creates a local `Stream` object, which uses the [`publish()`](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) method to publish local audio/video stream. |

## TRTC.Logger

TRTC.Logger provides methods for log settings such as [log output level](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.Logger.html#.LogLevel) setting and log upload enabling/disabling.

| API                                                                                                       | Description               |
| --------------------------------------------------------------------------------------------------------- | ------------------ |
| [setLogLevel](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.Logger.html#.setLogLevel) | Sets the log output level. |
| [enableUploadLog](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.Logger.html#.enableUploadLog) | Enables log upload.     |
| [disableUploadLog](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.Logger.html#.disableUploadLog) | Disables log upload. |

## Client

The audio/video call client object `Client` is created through [`createClient()`](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createClient) and represents an audio/video call.

| API                                                                                                       | Description                                                                                                                                                                            |
| --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [setProxyServer](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#setProxyServer)           | Sets proxy servers. This method is suitable where you deploy proxy servers, e.g., Nginx + Coturn, by yourself.                                                                                                      |
| [setTurnServer](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#setTurnServer) | Sets TURN servers. This method is used along with [`setProxyServer()`](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#setProxyServer) and is suitable where you deploy proxy and TURN servers by yourself. |
| [join](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join)                               | Enters a room, which starts an audio/video call. If the room does not exist, the system will create one.                                                                                |
| [leave](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#leave)                             | Exits the current room, which ends the current audio/video call.                                                                                                                                |
| [publish](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) | Publishes local audio/video stream. This method can be called only after room entry using the [`join()`](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join) method. Only one local stream can be published in one audio/video call.                    |
| [unpublish](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#unpublish)                     | Unpublishes local stream.                                                                                                                                                                |
| [subscribe](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#subscribe)                     | Subscribes to a remote stream.                                                                                                                                                                    |
| [unsubscribe](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#unsubscribe)                 | Unsubscribes from a remote stream.                                                                                                                                                                |
| [switchRole](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#switchRole)                   | Switches user roles. This method works only in the interactive live streaming mode (`live`).                                                                                                                                  |
| [on](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#on)                                   | Listens for client object events.                                                                                                                                                            |
| [getRemoteMutedState](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#getRemoteMutedState) | Gets the list of the audio/video mute status of remote users in the current room.                                                                                                                                    |
| [getLocalAudioStats](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#getLocalAudioStats) | Gets audio statistics of published local streams. This method can be used only after [`publish()`](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) is called.                                   |
| [getLocalVideoStats](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#getLocalVideoStats) | Gets video statistics of published local streams. This method can be used only after [`publish()`](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) is called.                                   |
| [getRemoteAudioStats](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#getRemoteAudioStats) | Gets audio statistics of all current remote streams.                                                                                                                                              |
| [getRemoteVideoStats](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#getRemoteVideoStats) | Gets video statistics of all current remote streams.                                                                                                                                              |

## LocalStream

LocalStream (local audio/video stream) is created through [`createStream`](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createStream) and is a subclass of [Stream](https://trtc-1252463788.file.myqcloud.com/web/docs/Stream.html).

| API                                                                                                            | Description                                                                                                                                                                                     |
| -------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [initialize](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize)                   | Initializes local audio/video stream objects.                                                                                                                                                                 |
| [setAudioProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setAudioProfile) | Sets audio profiles. This method can be used only before [initialize()](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) is called. |
| [setVideoProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setVideoProfile) | Sets video profiles. This method can be used only before [`initialize()`](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) is called. |
| [setScreenProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setScreenProfile) | Sets screen sharing profiles. This method can be used only before [`initialize()`](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) is called. |
| [setVideoContentHint](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setVideoContentHint) | Sets video content hints, mainly in order to improve the video encoding quality in different scenarios. This method can be used only after [`initialize()`](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) is called. |
| [switchDevice](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#switchDevice)               | Switches media input devices.                                                                                                                                                                       |
| [addTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#addTrack)                       | Adds an audio or video track.                                                                                                                                                                     |
| [removeTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#removeTrack)                 | Removes the video track.                                                                                                                                                                           |
| [replaceTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#replaceTrack)               | Replaces audio or video track.                                                                                                                                                                     |
| [play](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#play)                               | Starts playing audio/video stream.                                                                                                                                                                         |
| [stop](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#stop)                               | Stops playing audio/video stream.                                                                                                                                                                       |
| [resume](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#resume)                           | Resumes playing audio/video stream.                                                                                                                                                                         |
| [close](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#close)                             | Closes audio/video stream.                                                                                                                                                                           |
| [muteAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#muteAudio)                     | Disables the audio track.                                                                                                                                                                           |
| [muteVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#muteVideo)                     | Disables the video track.                                                                                                                                                                           |
| [unmuteAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#unmuteAudio)                 | Enables the audio track.                                                                                                                                                                           |
| [unmuteVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#unmuteVideo)                 | Enables the video track.                                                                                                                                                                           |
| [getId](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getId)                             | Gets the unique stream ID.                                                                                                                                                                |
| [getUserId](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getUserId)                     | Gets the ID of the user to whom the stream belongs.                                                                                                                                                                  |
| [setAudioOutput](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setAudioOutput)           | Sets the audio output device.                                                                                                                                                                       |
| [getAudioLevel](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getAudioLevel)             | Gets the current audio level. This method works only if there is audio data in local or remote stream.                                                                                                                               |
| [hasAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#hasAudio)                       | Specifies whether there is an audio track.                                                                                                                                                                       |
| [hasVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#hasVideo)                       | Specifies whether there is a video track.                                                                                                                                                                       |
| [getAudioTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getAudioTrack)             | Gets the audio track.                                                                                                                                                                           |
| [getVideoTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getVideoTrack)             | Gets the video track.                                                                                                                                                                           |
| [getVideoFrame](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getVideoFrame)             | Gets the current video frame.                                                                                                                                                                         |
| [on](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#on)                                   | Listens for stream events.                                                                                                                                                                       |



## RemoteStream

Remote audio/video stream, which is obtained by listening for the [Client.on('stream-added')](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html#.STREAM_ADDED) event and is a subclass of `[Stream]()`.

| API                                                                                                   | Description                                                                                               |
| ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| [getType](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getType) | Gets the remote stream type. This method is mainly used to determine whether a remote stream is a primary audio/video stream or secondary video stream (which is usually a screen sharing stream). |
| [play](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#play)                     | Starts playing audio/video stream.                                                                                   |
| [stop](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#stop)                     | Stops playing audio/video stream.                                                                                 |
| [resume](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#resume)                 | Resumes playing audio/video stream.                                                                                   |
| [close](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#close)                   | Closes audio/video stream.                                                                                     |
| [muteAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#muteAudio)           | Disables the audio track.                                                                                     |
| [muteVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#muteVideo)           | Disables the video track.                                                                                     |
| [unmuteAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#unmuteAudio)       | Enables the audio track.                                                                                     |
| [unmuteVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#unmuteVideo)       | Enables the video track.                                                                                     |
| [getId](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getId)                   | Gets the unique stream ID.                                                                          |
| [getUserId](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getUserId)           | Gets the ID of the user to whom the stream belongs.                                                                            |
| [setAudioOutput](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#setAudioOutput) | Sets the audio output device.                                                                                 |
| [setAudioVolume](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#setAudioVolume) | Sets the audio level.                                                                                 |
| [getAudioLevel](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getAudioLevel) | Gets the current audio level. This method works only if there is audio data in local or remote stream.                                         |
| [hasAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#hasAudio)             | Specifies whether there is an audio track.                                                                                 |
| [hasVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#hasVideo)             | Specifies whether there is a video track.                                                                                 |
| [getAudioTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getAudioTrack)   | Gets the audio track.                                                                                     |
| [getVideoTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getVideoTrack)   | Gets the video track.                                                                                     |
| [getVideoFrame](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getVideoFrame)   | Gets the current video frame.                                                                                   |
| [on](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#on)                         | Listens for stream events.                                                                                 |


## RtcError

`RtcError` object.

| API                                                                                 | Description         |
| ----------------------------------------------------------------------------------- | ------------ |
| [getCode](https://trtc-1252463788.file.myqcloud.com/web/docs/RtcError.html#getCode) | Gets the error code. |


