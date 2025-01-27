## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC’s video conferencing features, including screen sharing, beauty filters, and low-latency conferencing.

To quickly enable the video conferencing feature, you can modify the demo we provide and adapt it to your needs. You can also use the `TRTCMeeting` component and customize your own UI.

[](id:DemoUI)
## Using the Demo UI
[](id:ui.step1)
### Step 1. Create an application.
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g., `TestMeetingRoom`, and click **Create**.

>!The video conferencing feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the SDK and demo source code.
1. Download the SDK and demo source code for your platform.
2. Click **Next**.

[](id:ui.step3)
### Step 3. Configure demo project files.
1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Find and open the `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` file.
3. Set parameters in `GenerateTestUserSig.java` as follows.
<ul style="margin:0"><li/>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the demo.
Open the `TRTCScenesDemo` project with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the demo source code.
The `trtcmeetingdemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The table below lists the files (folders) and UI views they represent. You can refer to it when making UI changes.

| File or Folder | Use |
|:-------:|:--------|
| remote | The remote user list view |
| widget | Common UI component |
| CreateMeetingActivity.java | The meeting creation view |
| MeetingMainActivity.java | The main view for video conferencing |
| MeetingVideoView.java | Include `TXCloudVideoView`, which displays the video data of the local user and remote users |
| MemberEntity.java | User data at the UI layer |
| MemberListAdapter.java | Adapter for the main video conferencing view |

[](id:model)
## Implementing A Custom UI

The `trtcmeetingdemo` folder in the [source code](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtcmeetingdemo/src/main/java/com/tencent/liteav/meeting) contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCMeeting`. You can find the component’s API functions in `TRTCMeeting.java` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:model.step1)
### Step 1. Integrate the SDKs.
The video conferencing component `TRTCMeeting` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project.

**Method 1: adding dependencies via Maven**
1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
```
dependencies {
       compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       compile 'com.tencent.imsdk:imsdk:latest.release'
}
```
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).
>
2. In `defaultConfig`, specify the CPU architecture to be used by the app.
```
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
```
3. Click **Sync Now** to have the SDKs downloaded and integrated into your project automatically.

**Method 2: adding dependencies through local AAR files**
If your access to the Maven repository is slow, you can download the ZIP packages of the SDKs and manually and integrate them into your project as instructed in the documents below.
<table>
<tr>
<th>SDK</th>
<th>Download Page</th>
<th>Integration Guide</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">Integration document</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">Integration document</a></td>
</tr>
</table>

[](id:model.step2)
### Step 2. Configure permission requests and obfuscation rules.
Configure permission requests for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the camera and read storage permissions must be requested at runtime.)
```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```

In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
```
-keep class com.tencent.** { *; }
```

[](id:model.step3)
### Step 3. Import the `TRTCMeeting` component.
Copy all files in the following directory to your project:
```
src/main/java/com/tencent/liteav/meeting/model
```

<span id="model.step4"></span>
### Step 4. Create a component instance and log in.
1. Call the `sharedInstance` API to create an instance of the `TRTCMeeting` component.
2. Call the `setDelegate` function to register event callbacks of the component.
3. Call the `login` function to log in to the component. Set the key parameters as described below.
 <table>
<tr>
<th>Parameter</th>
<th>Note</th>
</tr>
<tr>
<td>SDKAPPID</td>
<td>You can view the `SDKAPPID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr>
<tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_).</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr>
<tr>
<td>callback</td>
<td>Login callback. The code is 0 if login is successful.</td>
</tr>
</table>
<dx-codeblock>
```
TRTCMeeting trtcMeeting = TRTCMeeting.sharedInstance(this);
trtcMeeting.login(SDKAPPID, userId, userSig, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //Login successful
        }
    }
});
```

[](id:model.step5)
### Step 5. Create a meeting as a host.
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo as a host.
2. Call `setDelegate` to create a meeting room via `createMeeting`.
3. Call `startCameraPreview` to capture video image and `startMicrophone` to capture sound.
4. To use beauty filters, you can add beauty filter buttons to the UI and set beauty filters through `getBeautyManager`.
>?Only the Enterprise Edition SDK supports face changing and stickers.
>
![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)


```
// 1. The host sets his or her nickname and profile photo.
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2. The host creates a room.
trtcMeeting.createMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. The host turns on the camera and enables audio capturing.
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            // 4. The host sets beauty filters.
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});
```

<span id="model.step6"></span>
### Step 6. Join a meeting as an attendee.
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo as an attendee.
2. Call `enterMeeting` and pass in the meeting room ID to enter the room.
3. Call `startCameraPreview` to capture video image and `startMicrophone` to capture sound.
4. If another attendee turns on the camera, you will receive the `onUserVideoAvailable` notification, and can call `startRemoteView` and pass in the `userId` to play the attendee’s video.

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```
// 1. The attendee sets his or her nickname and profile photo.
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2. The attendee calls `enterMeeting` to enter the meeting room.
trtcMeeting.enterMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. After entering the room, the attendee turns on the mic and camera, or enables beauty filters as well.
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});

// 3. The attendee receives a notification that another attendee has turned on the camera and starts playing the attendee’s video.
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onUserVideoAvailable(String userId, boolean available) {
        if (available) {
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startRemoteView(userId, txCloudVideoView);
        } else {
            trtcMeeting.stopRemoteView(userId, null);
        }
    }
});
```

[](id:model.step7)
### Step 7. Enable screen sharing.

1. The screen sharing feature requires the floating window permission, so you need to include the permission requesting logic in your UI.
2. Call `startScreenCapture`, pass in the encoding parameters and floating window to start screen sharing. For more information, see [TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58).
3. Other attendees in the room will receive the `onUserVideoAvailable` event notification.
>!Screen sharing and camera capturing are mutually exclusive. Before enabling screen sharing, you need to call `stopCameraPreview` to disable camera capturing.

```
// 1. Add the SDK’s screen sharing activity and permission in `AndroidManifest.xml`.
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<application>
    <activity
        android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity"
        android:theme="@android:style/Theme.Translucent" />
</application>

// 2. Request the floating window permission in your UI.
if (Build.VERSION.SDK_INT >= 23) {
    if (!Settings.canDrawOverlays(getApplicationContext())) {
        Intent intent = new Intent(Settings.ACTION_MANAGE_OVERLAY_PERMISSION, Uri.parse("package:" + getPackageName()));
        startActivityForResult(intent, 100);
    } else {
        startScreenCapture();
    }
} else {
    startScreenCapture();
}

// 3. System callback result
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == 100) {
        if (Build.VERSION.SDK_INT >= 23) {
            if (Settings.canDrawOverlays(this)) {
                // The user grant the permission.
                startScreenCapture();
            } else {
            }
        }
    }
}
// 4. Enable screen sharing.
private void startScreenCapture() {
        TRTCCloudDef.TRTCVideoEncParam encParams = new TRTCCloudDef.TRTCVideoEncParam();
        encParams.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720;
        encParams.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT;
        encParams.videoFps = 10;
        encParams.enableAdjustRes = false;
        encParams.videoBitrate = 1200;

        TRTCCloudDef.TRTCScreenShareParams params = new TRTCCloudDef.TRTCScreenShareParams();
        mTRTCMeeting.stopCameraPreview();
        mTRTCMeeting.startScreenCapture(encParams, params);
}
```

[](id:model.step8)
### Step 8. Implement text chat and muting notifications.
- Call `sendRoomTextMsg` to send text messages, and all hosts and attendees in the room will receive the `onRecvRoomTextMsg` callback.
 IM has its default content moderation rules. Text messages that contain blocked terms will not be forwarded by the cloud.
```
// Sender: send text messages
trtcMeeting.sendRoomTextMsg("Hello Word!", null);
// Recipient: listen for text messages
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomTextMsg(
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        Log.d(TAG, "Received a message from" + userInfo.userName + ":" + message);
    }
});
```
- Call `sendRoomCustomMsg` to send custom (signaling) messages, and all hosts and attendees in the room will receive the `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, such as muting notifications and notifications about other meeting controls.
```
// Sender: customize CMD to distinguish a muting notification
// E.g., use "CMD_MUTE_AUDIO" to indicate muting notifications
trtcMeeting.sendRoomCustomMsg("CMD_MUTE_AUDIO", "1", null);
// Receiver: listen for custom messages
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, 
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        if ("CMD_MUTE_AUDIO".equals(cmd)) {
            // Receive a muting notification.
            Log.d(TAG, "Received a muting notification from" + userInfo.userName + ":" + message);
            trtcMeeting.muteLocalAudio("1".equals(message));
        }
    }
});
```
