This document describes how to access and debug the GME APIs for Windows.

> ?This document applies to GME SDK v2.8.



## Key Considerations for Using GME

GME divides into two services: voice chat service and voice messaging and speech-to-text service.

![image](https://main.qcloudimg.com/raw/7a287c9cf60259eaea9469e110927462.png)

### Important APIs

| Important API | Description |
| ------------- | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| EnterRoom | Enters room (voice chat) |
| EnableMic | Enables mic (voice chat) |
| EnableSpeaker | Enables speaker (voice chat) |
| StartRecordingWithStreamingRecognition | Stream records audio and converts to text (voice messaging and speech-to-text) |

### Important notes

- Configure your project before using GME; otherwise, the SDK will not take effect.
- After a GME API is called successfully, `AV_OK` will be returned with the value being 0.
- GME APIs should be called in the same thread.
- The `Poll` API should be called periodically for GME to trigger event callbacks.
- For detailed error codes, please see [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223).

### C++ classes

| Class | Description |
| ------ | :----------: |
| ITMGContext | Key APIs |
| ITMGRoom | Room APIs |
| ITMGRoomManager | Room management APIs |
| ITMGAudioCtrl | Audio APIs |
| ITMGAudioEffectCtrl | Sound effect and accompaniment APIs |
| ITMGPTT | Voice messaging and speech-to-text APIs |

## Key APIs

Before the initialization, the SDK is in the uninitialized status, and you need to initialize it through the `Init` API before you can use the voice chat and voice messaging and speech-to-text services. **If you switch the account, please call `UnInit` to uninitialize the SDK.**

If you have any questions when using the service, please see [General FAQs](https://intl.cloud.tencent.com/document/product/607/30254).

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |


### Importing the header file

```
#include "auth_buffer.h"
#include "tmg_sdk.h"
#include "AdvanceHeaders/tmg_sdk_adv.h"
#include <vector>
```

### Callback

#### Setting callback sample

```
// When initializing the SDK
m_pTmgContext = ITMGContextGetInstance();
m_pTmgContext->SetTMGDelegate(this);

// In the destructor
CTMGSDK_For_AudioDlg::~CTMGSDK_For_AudioDlg()
{
			ITMGContextGetInstance()->SetTMGDelegate(NULL);
}

```

#### Message delivery

The API class uses the `Delegate` method to send callback notifications to the application. `ITMG_MAIN_EVENT_TYPE` indicates the message type. The data on Windows is in json string format. For the key-value pairs, please see the relevant documentation.

```
// Declaration in the header file
virtual void OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data);
// Sample code
void CTMGSDK_For_AudioDlg::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data)
{
			switch(eventType)
			{
			case ITMG_MAIN_EVENT_TYPE_XXXX_XXXX:
				{
					// Process the callback
				}
				break;
			}
}
```

### Getting singleton
The GME SDK is provided in the form of a singleton, all calls begin with `ITMGContext`, and callbacks are passed to the application through `ITMGDelegate`, which should be configured first.

#### Sample code  

```
ITMGContext* m_pTmgContext;
m_pTmgContext->Init(AppID, OpenID);
```



### Initializing SDK
- This API is used to initialize the GME service. It is recommended to call it when initializing the application.
- **For more information on how to get the `sdkAppId` parameter, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/10782)**.
- **The openID uniquely identifies a user with the rules stipulated by the application developer and must be greater than 10,000 and unique in the application (currently, only INT64 is supported)**.

> !The SDK must be initialized before an user can enter a voice chat room.

#### Function prototype

```
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
```

| Parameter | Type | Description |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | char* | `AppId` provided by the GME service from the [Tencent Cloud Console](https://console.cloud.tencent.com/) |
| openId | char* | `OpenId` can only be in Int64 type (converted to string) with **a value greater than 10,000; otherwise, initialization and room entry will fail**. |

| Returned Value | Description |
| ------------------------------- | --------------------------------------------- |
| AV_OK = 0 | Initialized SDK successfully. |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | Checks whether the SDK file is complete. It is recommended to delete it and then import the SDK again. |

The returned value `AV_ERR_SDK_NOT_FULL_UPDATE` is only a reminder but will not cause an initialization failure.

- If this error is reported during integration, please check the integrity and version of the SDK file as prompted.
- If this error is returned after executable file export, please ignore it and try to avoid displaying it in the UI.

#### Sample code 


```
#define SDKAPPID3RD "1400089356"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
```


### Triggering event callback

Event callbacks can be triggered by periodically calling the `Poll` API in `update`. The `Poll` API should be called periodically for GME to trigger event callbacks; otherwise, the entire SDK service will run exceptionally.
You can refer to the `EnginePollHelper.cpp` file in the demo.

#### Function prototype

```
class ITMGContext {
protected:
    virtual ~ITMGContext() {}
    
public:    	
	virtual void Poll()= 0;
}

```

#### Sample code

```
// Declaration in the header file

// Code implementation
void TMGTestScene::update(float delta)
{
    ITMGContextGetInstance()->Poll();
}
```

### Pausing system

When a `Pause` event occurs in the system, the engine should also be notified for pause.

#### Function prototype

```
ITMGContext int Pause()
```

### Resuming system

When a `Resume` event occurs in the system, the engine should also be notified for resumption. The `Resume` API only supports resuming voice chat.

#### Function prototype

```
ITMGContext int Resume()
```



### Uninitializing SDK

This API is used to uninitialize the SDK to make it uninitialized. **Switching accounts requires uninitialization**.

#### Function prototype

```
ITMGContext int Uninit()
```


## Voice Chat
Voice chat refers to the one-to-one or one-to-many real-time voice call feature.

### Voice chat flowchart

![](https://main.qcloudimg.com/raw/e536525aa47c06a5a84bb6c8d4851b22.png)



### Voice chat room call flowchart

![](https://main.qcloudimg.com/raw/a61ca1d7cdecf09bd223766b2a5cd69f.png)

## Voice Chat Room APIs

You should initialize and call the SDK to enter a room before voice chat can start.
If you have any questions when using the service, please see [FAQs About Voice Chat](https://intl.cloud.tencent.com/document/product/607/30257).


| API | Description |
| -------------- | :------------------: |
| GenAuthBuffer | Initializes authentication |
| EnterRoom | Enters room |
| IsRoomEntered | Indicates whether room entry is successful |
| ExitRoom | Exits room |
| ChangeRoomType | Modifies user's room audio type |
| GetRoomType | Gets user's room audio type |

### Authentication information

Generate `AuthBuffer` for encryption and authentication of relevant features. For release in the production environment, please use the backend deployment key as detailed in [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218).    
To get authentication for voice messaging and speech-to-text, the room ID parameter must be set to `null`.

#### Function prototype

```
int  QAVSDK_AuthBuffer_GenAuthBuffer(unsigned int dwSdkAppID, const char* strRoomID, const char* strOpenID,
	const char* strKey, unsigned char* strAuthBuffer, unsigned int bufferLength);
```

| Parameter | Type | Description |
| ------ | :----: | ------------------------------------------------------------ |
| dwSdkAppID | int | `AppId` from the Tencent Cloud console. |
| strRoomID | char* | Room ID, which can contain up to 127 characters (for voice messaging and speech-to-text service, enter `null`). |
| strOpenID | char* | User ID, which is the same as `openID` during initialization. |
| strKey | char* | Permission key from the Tencent Cloud [Console](https://console.cloud.tencent.com/gamegme) |
| strAuthBuffer | char* | Returned `authbuff` |
| bufferLength | int | Length of the `authbuff` passed in. 500 is recommended. |



#### Sample code  

```
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
```



### Entering room

When a user enters a room with the generated authentication information, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` message will be received as a callback. Mic and speaker are not enabled by default after room entry. The returned value of `AV_OK` indicates a success.

#### Function prototype

```
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| roomId | char* | Room ID, which can contain up to 127 characters |
| roomType | ITMG_ROOM_TYPE | Room audio type |
| authBuffer | char* | Authentication key |
| buffLen | int | Authentication key length |

For more information on how to choose a room audio type, please see [Sound Quality Selection](https://intl.cloud.tencent.com/document/product/607/18522).

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
```

### Callback for room entry
After the user enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function for callback and processing.

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
					switch (eventType) {
						case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
						{
							ListMicDevices();
							ListSpeakerDevices();

							std::string strText = "EnterRoom complete: ret=";
							strText += data;
							m_EditMonitor.SetWindowText(MByteToWChar(strText).c_str());
							}
					}
}
```

#### Data details

| Message | Data | Sample |
| ------------------------------- | :----------------: | ---------------------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM | result; error_info | {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info |{"error_info":"waiting timeout, please check your network","result":0}  |


#### Error codes

| Error Code Value | Cause and Suggested Solution |
| -------- | ------------------------------------------------------------ |
| 7006 | Authentication failed. Possible causes: 1. The `AppID` does not exist or is incorrect. 2. An error occurred while authenticating the `authbuff`. 3. Authentication expired. 4. The `openID` is non-compliant. |
| 7007 | Already in another room. |
| 1001 | The user was already in the process of entering a room but repeated this operation. It is recommended not to call the room entering API until the room entry callback is returned. |
| 1003 | The user was already in the room and called the room entering API again. |
| 1101 | Make sure that the SDK is initialized, `OpenId` complies with the rules, the APIs are called in the same thread, and the `Poll` API is called normally. |

### Determining whether user has entered room

This API is used to determine whether the user has entered a room. A bool-type value will be returned.

#### Function prototype  

```
ITMGContext virtual bool IsRoomEntered()
```

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->IsRoomEntered();
```

### Exiting room

This API is called to exit the current room. It is an async API. The returned value of `AV_OK` indicates a successful async delivery.

> !If there is a scenario in the application where room entry is performed immediately after room exit, you don't need to wait for the `RoomExitComplete` callback notification from the `ExitRoom` API during API call; instead, you can directly call the API.

#### Function prototype  

```
ITMGContext virtual int ExitRoom()
```

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();
```

### Callback for room exit

After the user exits a room, a callback will be returned with the message being `ITMG_MAIN_EVENT_TYPE_EXIT_ROOM`.

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
switch (eventType) {
					case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
					{
						// Process
						break;
						}
					}
}
```

#### Data details

| Message | Data | Sample |
| ------------------------------ | :----------------: | ---------------------------- |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | result; error_info | {"error_info":"","result":0} |

### Modifying user's room audio type

This API is used to modify a user's room audio type. For the result, please see the callback event. The event type is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE`. The audio type of the room is determined by the first user to enter the room. After that, if a member in the room changes the room type, it will take effect for all members there.

#### Function prototype  

```
IITMGContext TMGRoom public int ChangeRoomType((ITMG_ROOM_TYPE roomType)
```

| Parameter | Type | Description |
| --------- | :--: | ----------------------------------------------------- |
| roomType | ITMG_ROOM_TYPE | Room type to be switched to. For room audio types, please see the `EnterRoom` API. |

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->ChangeRoomType(ITMG_ROOM_TYPE_FLUENCY);
```

### Getting user's room audio type

This API is used to get a user's room audio type. The returned value is the room audio type. Value 0 indicates that an error occurred while getting the user's room audio type. For room audio types, please see the `EnterRoom` API.

#### Function prototype  

```
IITMGContext TMGRoom public  int GetRoomType()
```

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
ITMGContextGetInstance()->GetRoom()->GetRoomType();
```

### Callback for room type setting completion

After the room type is set, the event message `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE` will be returned in the callback. The returned parameters include `result`, `error_info`, and `new_room_type`. The `new_room_type` represents the following information. The event message will be identified in the `OnEvent` function.

| Event Subtype | Parameter | Description |
| -------------------------------- | :------: | ------------------------------------------------------------ |
| ITMG_ROOM_CHANGE_EVENT_ENTERROOM | 1 | Indicates that the existing audio type is inconsistent with and changed to that of the entered room. |
| ITMG_ROOM_CHANGE_EVENT_START | 2 | Indicates that a user is already in the room and the audio type starts changing (e.g., calling the `ChangeRoomType` API to change the audio type). |
| ITMG_ROOM_CHANGE_EVENT_COMPLETE | 3 | Indicates that a user is already in the room and the audio type has been changed. |
| ITMG_ROOM_CHANGE_EVENT_REQUEST | 4 | Indicates that a room member calls the `ChangeRoomType` API to request a change of room audio type. |

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data) {
					if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE == type)
								{
						// Process room type events
					 }
}
```

#### Data details

| Message | Data | Sample |
| ------------------------------------- | :-------------------------------: | ---------------------------------------------- |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | result; error_info; new_room_type | {"error_info":"","new_room_type":0,"result":0} |

### Member status change

Notification for this event will be sent only when the status changes. To get member status in real time, cache the notification when it is received at a higher layer. The event message is `ITMG_MAIN_EVNET_TYPE_USER_UPDATE`, where the data contains `event_id` and `user_list`. The event message will be identified in the `OnEvent` function.
Notifications for audio events are subject to a threshold, and a notification will be sent only when this threshold is exceeded. The notification "A member has stopped sending audio packets" will be sent if no audio packets are received in more than two seconds.


| event_id | Description | Maintenance |
| ---------------------------- | :------------------: | ---------------------- |
| ITMG_EVENT_ID_USER_ENTER | A member enters the room | Member list |
| ITMG_EVENT_ID_USER_EXIT | A member exits the room | Member list |
| ITMG_EVENT_ID_USER_HAS_AUDIO | A member sends audio packets. This event can be used to determine whether a user is speaking and display the voiceprint effect | Chat member list |
| ITMG_EVENT_ID_USER_NO_AUDIO | A member stops sending audio packets | Chat member list |

#### Room member maintenance flowchart

![](https://main.qcloudimg.com/raw/50ef1ceda14eb244e434b8cbe85da5f3.png)

#### Sample code
```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
	switch (eventType) {
            case ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
		{
		// Process
		// Parse the parameter to get `eventID` and `user_list`
		    switch (eventID)
 		    {
 		    case ITMG_EVENT_ID_USER_ENTER:
  			    // A member enters the room
  			    break;
 		    case ITMG_EVENT_ID_USER_EXIT:
  			    // A member exits the room
			    break;
		    case ITMG_EVENT_ID_USER_HAS_AUDIO:
			    // A member sends audio packets
			    break;
		    case ITMG_EVENT_ID_USER_NO_AUDIO:
			    // A member stops sending audio packets
			    break;
 		    default:
			    break;
		    }
		break;
		}
	}
}
```

#### Data details

| Message | Data | Sample |
| ------------------------------------- | :-------------------------------: | ---------------------------------------------- |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | event_id; user_list| {"event_id":0,"user_list":""} |

### Room call quality control event

The message for quality control event triggered once every two seconds after room entry is `ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY`. The returned parameters include `weight`, `loss`, and `delay`, which represent the following information.

| Parameter | Type | Description |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int | Value range: 1-50. 50 indicates excellent sound quality, 1 indicates very poor (barely usable) sound quality, and 0 represents an initial meaningless value. Generally, if the value is below 30, you can remind users that the network is poor and recommend them to switch the network. |
| loss | double | Upstream packet loss rate |
| delay | int | Voice chat delay in ms |


## Voice Chat Audio APIs

![Image](https://main.qcloudimg.com/raw/863e0c165c7d43f9db59066befaac1e4.png)

### Notes on voice chat audio connection

The voice chat APIs can only be called after SDK initialization and room entry.
When Enable/Disable Mic/Speaker is clicked on the UI, the following practices are recommended:

- **For most game applications, it is recommended to call the `EnableMic` and `EnableSpeaker` APIs**, which is equivalent to calling the `EnableAudioCaptureDevice/EnableAudioSend` and `EnableAudioPlayDevice/EnableAudioRecv` APIs.
- For other mobile applications (such as social networking applications), enabling/disabling a capturing device will restart both capturing and playback devices. If the application is playing back background music, it will also be interrupted. Playback won't be interrupted if the mic is enabled/disabled through control of upstreaming/downstreaming. **Calling method: call `EnableAudioCaptureDevice(true)` and `EnableAudioPlayDevice(true)` once after room entry, and call `EnableAudioSend/Recv` to send/receive audio streams when Enable/Disable Mic is clicked**.
- For more information on how to release only a capturing or playback device, please see the `EnableAudioCaptureDevice` and `EnableAudioPlayDevice`.
- Call the `pause` API to pause the audio engine and call the `resume` API to resume the audio engine.

### Voice chat audio APIs

| API | Description |
| --------------------------- | :----------------------------: |
| GetMicListCount | Gets the number of mics |
| GetMicList | Enumerates mics |
| GetSpeakerListCount | Gets the number of speakers |
| GetSpeakerList | Enumerates speakers |
| SelectMic | Selects mic |
| SelectSpeaker | Selects speakers |
| EnableMic | Enables/disables mic |
| GetMicState | Gets mic status |
| EnableAudioCaptureDevice | Enables/disables capturing device |
| IsAudioCaptureDeviceEnabled | Gets capturing device status |
| EnableAudioSend | Enables/disables audio upstreaming |
| IsAudioSendEnabled | Gets audio upstreaming status |
| GetMicLevel | Gets real-time mic volume level |
| GetSendStreamLevel | Gets real-time audio upstreaming volume level |
| SetMicVolume | Sets mic volume level |
| GetMicVolume | Gets mic volume level |
| EnableSpeaker | Enables/disables speaker |
| GetSpeakerState | Gets speaker status |
| EnableAudioPlayDevice | Enables/disables playback device |
| IsAudioPlayDeviceEnabled | Gets playback device status |
| EnableAudioRecv | Enables/disables audio downstreaming |
| IsAudioRecvEnabled | Gets audio downstreaming status |
| GetSpeakerLevel | Gets real-time speaker volume level |
| GetRecvStreamLevel | Gets real-time downstreaming audio levels of other members in room |
| SetSpeakerVolume | Sets speaker volume level |
| GetSpeakerVolume | Gets speaker volume level |
| EnableLoopBack | Enables/disables in-ear monitoring |

## Voice Chat Capturing APIs

### Getting the number of mics
This API is used to get the number of mics.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetMicListCount()
```

#### Sample code

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicListCount();
```

### Enumerating mics
This API is used together with the `GetMicListCount` API to enumerate mics.

#### Function prototype 

```
ITMGAudioCtrl virtual int GetMicList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
				public:
					const char* pDeviceID;
					const char* pDeviceName;
};
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| ppDeviceInfoList | TMGAudioDeviceInfo | Device list |
| nCount | int | Gets the number of mics |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicList(ppDeviceInfoList,nCount);
```



### Selecting mic
This API is used to select a mic. If this API is not called or `DEVICEID_DEFAULT` is passed in, the default mic will be selected. The device ID is from the list returned by `GetMicList`.

#### Function prototype  

```
ITMGAudioCtrl virtual int SelectMic(const char* pMicID)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| pMicID | char* | Mic device ID |

#### Sample code  

```
const char* pMicID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectMic(pMicID);
```

### Enabling or disabling mic

This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

EnableMic = EnableAudioCaptureDevice + EnableAudioSend


#### Function prototype  

```
ITMGAudioCtrl virtual int EnableMic(bool bEnabled)
```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| bEnabled | bool | To enable the mic, set this parameter to `true`, otherwise set it to `false`. |

#### Sample code  

```
// Enable mic
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
```

### Getting mic status

This API is used to get the mic status. The returned value 0 indicates that the mic is off, while 1 on.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetMicState()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicState();
```

### Enabling or disabling capturing device

This API is used to enable/disable a capturing device. The device is not enabled by default after room entry.

- This API can only be called after room entry. The device will be disabled automatically after room exit.
- Operations such as permission application and volume type adjustment will generally be performed when a capturing device is enabled on a mobile device.

#### Function prototype  

```
ITMGContext virtual int EnableAudioCaptureDevice(bool enable)
```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| enable | bool | To enable the capturing device, set this parameter to `true`, otherwise set it to `false`. |

#### Sample code

```
// Enable capturing device
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioCaptureDevice(true);
```

### Getting capturing device status

This API is used to get the status of a capturing device.

#### Function prototype

```
ITMGContext virtual bool IsAudioCaptureDeviceEnabled()
```

#### Sample code

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioCaptureDeviceEnabled();
```

### Enabling or disabling audio upstreaming

This API is used to enable/disable audio upstreaming. If a capturing device is already enabled, it will send captured audio data; otherwise, it will remain mute. For more information on how to enable/disable the capturing device, please see the `EnableAudioCaptureDevice` API.

#### Function prototype

```
ITMGContext  virtual int EnableAudioSend(bool bEnable)
```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| enable | bool | To enable the audio upstream, set this parameter to `true`, otherwise set it to `false`. |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioSend(true);
```

### Getting audio upstreaming status

This API is used to get the status of audio upstreaming.

#### Function prototype  

```
ITMGContext virtual bool IsAudioSendEnabled()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioSendEnabled();

```

### Getting real-time mic volume level

This API is used to get the real-time mic volume level. An int-type value in the range of 0-100 will be returned. It is recommended to call this API once every 20 ms.

>?This API is not applicable to the voice messaging service.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetMicLevel()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicLevel();
```

### Getting real-time audio upstreaming volume level

This API is used to get the local real-time audio upstreaming volume level. An int-type value in the range of 0-100 will be returned.
>?This API is not applicable to the voice messaging service.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSendStreamLevel()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSendStreamLevel();
```

### Setting mic software volume level

This API is used to set the mic volume level. The corresponding parameter is `volume`, which is equivalent to attenuating or gaining the captured sound. 0 indicates that the audio is mute, while 100 indicates that the volume level remains unchanged. The default value is 100.
>?This API is not applicable to the voice messaging service.
>
#### Function prototype  

```
ITMGAudioCtrl virtual int SetMicVolume(int vol)
```

| Parameter | Type | Description |
| ------ | :--: | -------------------- |
| vol | int | Volume level. Value range: 0-200 |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->SetMicVolume(vol);
```
### Getting mic software volume level

This API is used to get the mic volume level. An int-type value will be returned. 101 indicates that the `SetMicVolume` API has not been called.
>?This API is not applicable to the voice messaging service.
>
#### Function prototype  
```
ITMGAudioCtrl virtual int GetMicVolume()
```
#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetMicVolume();
```
## Voice Chat Playback APIs


### Getting the number of speakers
This API is used to get the number of speakers.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerListCount()
```
#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerListCount();
```

### Enumerating speakers
This API is used together with the `GetSpeakerListCount` API to enumerate speakers.

#### Function prototype  
```
ITMGAudioCtrl virtual int GetSpeakerList(TMGAudioDeviceInfo* ppDeviceInfoList, int nCount)

class TMGAudioDeviceInfo
{
				public:
					const char* pDeviceID;
					const char* pDeviceName;
};
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| ppDeviceInfoList | TMGAudioDeviceInfo | Device list |
| nCount | int | Number of speakers obtained |

#### Sample code  
```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerList(ppDeviceInfoList,nCount);
```

### Selecting speaker
This API is used to select a playback device. If this API is not called or `DEVICEID_DEFAULT` is passed in, the default playback device will be selected. The device ID is from the list returned by `GetSpeakerList`.

#### Function prototype  
```
ITMGAudioCtrl virtual int SelectSpeaker(const char* pSpeakerID)
```

| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| pSpeakerID | char* | Speaker device ID |

#### Sample code  
```
const char* pSpeakerID ="{0.0.1.00000000}.{7b0b712d-3b46-4f7a-bb83-bf9be4047f0d}";
ITMGContextGetInstance()->GetAudioCtrl()->SelectSpeaker(pSpeakerID);
```

### Enabling or disabling speaker

This API is used to enable/disable the speaker.
**If accompaniment is used, please call this API as instructed in [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504).**

EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv

#### Function prototype  

```
ITMGAudioCtrl virtual int EnableSpeaker(bool enabled)
```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| enable | bool | To disable the speaker, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
// Enable the speaker
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
```

### Getting speaker status

This API is used to get the speaker status. 0 indicates that the speaker is off, 1 on, and 2 working.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerState()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerState();
```



### Enabling or disabling playback device

This API is used to enable/disable a playback device.

#### Function prototype  

```
ITMGContext virtual int EnableAudioPlayDevice(bool enable) 
```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| enable | bool | To disable the playback device, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioPlayDevice(true);
```

### Getting playback device status

This API is used to get the status of a playback device.

#### Function prototype

```
ITMGContext virtual bool IsAudioPlayDeviceEnabled()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioPlayDeviceEnabled();
```

### Enabling or disabling audio downstreaming

This API is used to enable/disable audio downstreaming. If a playback device is already enabled, it will play back audio data from other members in the room; otherwise, it will remain mute. For more information on how to enable/disable the playback device, please see the `EnableAudioPlayDevice` API.

#### Function prototype  

```
ITMGContext virtual int EnableAudioRecv(bool enable)
```

| Parameter | Type | Description |
| --------- | :-----: | ------------------------------------------------------------ |
| enable | bool | To enable audio downstream, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableAudioRecv(true);
```



### Getting audio downstreaming status

This API is used to get the status of audio downstreaming.

#### Function prototype  

```
ITMGContext virtual bool IsAudioRecvEnabled() 
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->IsAudioRecvEnabled();
```

### Getting real-time speaker volume level

This API is used to get the real-time speaker volume level. An int-type value will be returned to indicate the volume level. It is recommended to call this API once every 20 ms.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerLevel()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerLevel();
```

### Getting the real-time downstreaming audio levels of other members in room

This API is used to get the real-time audio downstreaming volume levels of other members in the room. An int-type value will be returned. Value range: 0-200.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetRecvStreamLevel(const char* openId)
```

| Parameter | Type | Description |
| ------ | :----: | -------------------- |
| openId | char* | `openId` of another member in the room |

#### Sample code  

```
iter->second.level = ITMGContextGetInstance()->GetAudioCtrl()->GetRecvStreamLevel(iter->second.openid.c_str());
```

### Setting speaker volume level

This API is used to set the speaker volume level.
The corresponding parameter is volume. 0 indicates that the audio is mute, while 100 indicates that the volume level remains unchanged. The default value is 100.

#### Function prototype  

```
ITMGAudioCtrl virtual int SetSpeakerVolume(int vol)
```

| Parameter | Type | Description |
| ------ | :--: | -------------------- |
| vol | int | Volume level. Value range: 0-200 |

#### Sample code  

```
int vol = 100;
ITMGContextGetInstance()->GetAudioCtrl()->SetSpeakerVolume(vol);
```

### Getting speaker volume level

This API is used to get the speaker volume level. An int-type value will be returned to indicate the volume level. 101 indicates that the `SetSpeakerVolume` API has not been called.
`Level` indicates the real-time volume level, while `Volume` the speaker volume level. The final volume level equals to Level*Volume%.
For example, if the value of "Level" is 100 and that of “Volume” is 60, then the final volume level will be 60.

#### Function prototype  

```
ITMGAudioCtrl virtual int GetSpeakerVolume()
```

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->GetSpeakerVolume();
```

### Enabling in-ear monitoring

This API is used to enable in-ear monitoring. You need to call `EnableLoopBack+EnableSpeaker` before you can hear your own voice.

#### Function prototype  

```
ITMGAudioCtrl virtual int EnableLoopBack(bool enable)
```

| Parameter | Type | Description |
| ------ | :-----: | ------------ |
| enable | bool | Specifies whether to enable |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->EnableLoopBack(true);
```

## Voice Messaging and Speech-to-Text

Voice messaging refers to recording and sending a voice message. At the same time, the voice message can be converted to text and translated.

>?It is recommended to use the streaming voice-to-text service.

### Voice messaging and speech-to-text conversion flowchart

<img src="https://main.qcloudimg.com/raw/310eaf2b780c5fc47ffeaf791a6df392.png" width="70%">



## Accessing Voice Messaging and Speech-to-Text Service

### Voice messaging and speech-to-text APIs

| API | Description |
| -------------------------------------- | :------------------------: |
| ApplyPTTAuthbuffer | Initializes authentication |
| SetMaxMessageLength | Specifies maximum length of voice message |
| StartRecording | Starts recording |
| StartRecordingWithStreamingRecognition | Starts streaming recording |
| PauseRecording | Pauses recording |
| ResumeRecording | Resumes recording |
| StopRecording | Stops recording |
| CancelRecording | Cancels recording |
| GetMicLevel | Gets real-time mic volume level |
| SetMicVolume | Sets recording volume level |
| GetMicVolume | Gets recording volume level |
| GetSpeakerLevel | Gets real-time speaker volume level |
| SetSpeakerVolume | Sets playback volume level |
| GetSpeakerVolume | Gets playback volume level |
| UploadRecordedFile | Uploads audio file |
| DownloadRecordedFile | Downloads audio file |
| PlayRecordedFile | Plays back audio |
| StopPlayFile | Stops playing back audio |
| GetFileSize | Gets audio file size |
| GetVoiceFileDuration | Gets audio file duration |
| SpeechToText | Converts speech to text |


### Initializing SDK

Before the initialization, the SDK is in the uninitialized status, and you need to initialize it through the `Init` API before you can use the voice chat and voice messaging and speech-to-text services.

If you have any questions when using the service, please see [Voice Messaging and Speech-to-Text](https://intl.cloud.tencent.com/document/product/607/30258).

### Initialization APIs

| API | Description |
| ------ | :----------: |
| Init | Initializes GME |
| Poll | Triggers event callback |
| Pause | Pauses the system |
| Resume | Resumes the system |
| Uninit | Uninitializes GME |



### Authentication initialization

Call authentication initialization after initializing the SDK. For more information on how to get the `authBuffer`, please see `QAVSDK_AuthBuffer_GenAuthBuffer` (the voice chat authentication information API).

#### Function prototype  

```
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
```

| Parameter | Type | Description |
| ---------- | :----: | ---- |
| authBuffer | char* | Authentication |
| authBufferLen | int | Authentication length |

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
```


## Streaming Speech Recognition


### Starting streaming speech recognition

This API is used to start streaming speech recognition. Text obtained from speech-to-text conversion will be returned in real time in its callback. It can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation. **To stop recording, call `StopRecording`**.

#### Function prototype  

```
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage) 
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | char* | Path of stored audio file |
| speechLanguage | char* | The language in which the audio file is to be converted to text. For parameters, please see [ Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) |
| translateLanguage | char* | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) (This parameter is currently unavailable. Enter the same value as that of `speechLanguage`) |

#### Sample code  
```
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```

### Callback for streaming speech recognition
After streaming speech recognition is started, you need to listen for callback messages in the callback function `onEvent`. Event messages are divided into:
- `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE` returns text after the recording is stopped and the recognition is completed, which is equivalent to returning the recognized text after a paragraph of speech.
- `ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING` returns the recognized text in real-time during the recording, which is equivalent to returning the recognized text while speaking.
The event message will be identified in the `OnEvent function` based on the actual needs. The passed parameters include the following four messages.

| Message Name | Description |
| ------------- |:-------------:|
| result | Returns code indicating whether streaming speech recognition is successful. |
| text | Text converted from speech |
| file_path | Local path of stored recording file |
| file_id | Backend URL address of recording file, which will be retained for 90 days |

>!The file_id is empty when the 'ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING' message is listened.

#### Error codes

| Error Code | Description | Suggested Solution |
| ------------- |:-------------:|:-------------:|
| 32775 | Streaming speech-to-text conversion failed, but recording succeeded.| Call the `UploadRecordedFile` API to upload the recording file and then call the `SpeechToText` API to perform speech-to-text conversion. |
| 32777 | Streaming speech-to-text conversion failed, but recording and upload succeeded.| The message returned contains a backend URL after successful upload. Call the `SpeechToText` API to perform speech-to-text conversion. |
| 32786 | Streaming speech-to-text conversion failed. | During streaming recording, wait for the execution result of the streaming recording API to return. |

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
					switch (eventType) {
						case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
						{
							HandleSTREAM2TEXTComplete(data,true);
							break;
						}
						...
						case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING:
						{
							HandleSTREAM2TEXTComplete(data, false);
							break;
						}
					}
}

void CTMGSDK_For_AudioDlg::HandleSTREAM2TEXTComplete(const char* data, bool isComplete)
{
					std::string strText = "STREAM2TEXT: ret=";
					strText += data;
					m_EditMonitor.SetWindowText(MByteToWChar(strText).c_str());
					Json::Reader reader;
					Json::Value root;
					bool parseRet = reader.parse(data, root);
					if (!parseRet) {
						::SetWindowText(m_EditInfo.GetSafeHwnd(),MByteToWChar(std::string("parse result Json error")).c_str());
					}
						else
						{
							if (isComplete) {
												::SetWindowText(m_EditUpload.GetSafeHwnd(), MByteToWChar(root["file_id"].asString()).c_str());
											}
											else {
													std::string isruning = "STREAMINGRECOGNITION_IS_RUNNING";
													::SetWindowText(m_EditUpload.GetSafeHwnd(), MByteToWChar(isruning).c_str());
												 }
					}
}
```



## Voice Message Recording

### Specifying maximum duration of voice message

This API is used to specify the maximum duration of a voice message, which can be up to 58 seconds.

#### Function prototype

```
ITMGPTT virtual int SetMaxMessageLength(int msTime)
```

| Parameter | Type | Description |
| ------ | :--: | ------------------------------------------------ |
| msTime | int | Audio duration in ms. Value range: 1000 < msTime <= 58000 |

#### Sample code  

```
int msTime = 10000;
ITMGContextGetInstance()->GetPTT()->SetMaxMessageLength(msTime);
```

### Starting recording

This API is used to start recording. The recording file must be uploaded first before you can perform operations such as speech-to-text conversion.

#### Function prototype  

```
ITMGPTT virtual int StartRecording(const char* fileDir)
```

| Parameter | Type | Description |
| -------- | :----: | -------------- |
| fileDir | char* | Path of stored audio file |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->StartRecording(fileDir);
```

### Callback for recording start

The callback function `OnEvent` will be called after recording is started. The event message `ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameter includes `result` and `file_path`.

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ------------------------ | ------------------------------------------------------------ |
| 4097 | Parameter is empty. | Check whether the API parameters in the code are correct. |
| 4098 | Initialization error. | Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal. |
| 4099 | Recording is in progress. | Ensure that the SDK recording feature is used at the right time. |
| 4100 | Audio data is not captured. | Check whether the mic is working properly. |
| 4101 | An error occurred while accessing the file during recording. | Ensure the existence of the file and the validity of the file path. |
| 4102 | The mic is not authorized. | Mic permission is required for using the SDK. To add the permission, please see the SDK project configuration document for the corresponding engine or platform. |
| 4103 | The recording duration is too short. | The recording duration should be in ms and longer than 1,000 ms. |
| 4104 | No recording operation is started. | Check whether the recording starting API has been called. |

#### Sample code  

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
				switch (eventType) {
					case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
					{
					// Process
					break;
						}
					...
							case ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE:
					{
					// Process
					break;
					}
				}
}
```


### Pausing recording

This API is used to pause recording. If you want to resume recording, please call the `ResumeRecording` API.

#### Function prototype  

```
ITMGPTT virtual int PauseRecording()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->PauseRecording();
```

### Resuming recording

This API is used to resume recording.

#### Function prototype  

```
ITMGPTT virtual int ResumeRecording()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->ResumeRecording();
```

### Stopping recording

This API is used to stop recording. It is async, and a callback for recording completion will be returned after recording stops. A recording file will be available only after recording succeeds.

#### Function prototype  

```
ITMGPTT virtual int StopRecording()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->StopRecording();
```



### Canceling recording

This API is used to cancel recording. There is no callback after cancellation.

#### Function prototype  

```
ITMGPTT virtual int CancelRecording()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->CancelRecording();
```

### Getting the real-time mic volume level of voice messaging

This API is used to get the real-time mic volume level. An int-type value will be returned. Value range: 0-200.
>?This API is different from the voice chat API and is in `ITMGPTT.java`.

#### Function prototype  

```
ITMGPTT virtual int GetMicLevel()
```

#### Sample code  

```
ITMGContext.GetInstance(this).GetPTT().GetMicLevel();

```

### Setting the recording volume level of voice messaging

This API is used to set the recording volume level of voice messaging. Value range: 0-200.
>?This API is different from the voice chat API and is in `ITMGPTT.java`.

#### Function prototype  

```
ITMGPTT virtual int SetMicVolume(int vol)
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SetMicVolume(100);
```

### Getting the recording volume level of voice messaging

This API is used to get the recording volume level of voice messaging. An int-type value will be returned. Value range: 0-200.
>?This API is different from the voice chat API and is in `ITMGPTT.java`.

#### Function prototype  

```
ITMGPTT virtual int GetMicVolume()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetMicVolume();
```

### Getting the real-time speaker volume level of voice messaging

This API is used to get the real-time speaker volume level. An int-type value will be returned. Value range: 0-200.
>?This API is different from the voice chat API and is in `ITMGPTT.java`.

#### Function prototype  

```
ITMGPTT virtual int GetSpeakerLevel()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetSpeakerLevel();
```

### Setting the playback volume level of voice messaging

This API is used to set the playback volume level of voice messaging. Value range: 0-200.
>?This API is different from the voice chat API and is in `ITMGPTT.java`.

#### Function prototype  

```
ITMGPTT virtual int SetSpeakerVolume(int vol)
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SetSpeakerVolume(100);
```

### Getting the playback volume level of voice messaging

This API is used to get the playback volume level of voice messaging. An int-type value will be returned. Value range: 0-200.
>?This API is different from the voice chat API and is in `ITMGPTT.java`.

#### Function prototype  

```
ITMGPTT virtual int GetSpeakerVolume()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetSpeakerVolume();
```

## Voice Message Playback
### Playing back audio

This API is used to play back audio.

#### Function prototype  

```
ITMGPTT virtual int PlayRecordedFile(const char* filePath)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| filePath | char* | Local audio file path |

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------- | ------------------------------ |
| 20485 | Playback is not started. | Ensure the existence of the file and the validity of the file path. |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->PlayRecordedFile(filePath);
```

### Callback for audio playback

After the audio is played back, the event message `ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameter includes `result` and `file_path`.

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| 20481 | Initialization error. | Check whether the device is being used, whether the permissions are normal, and whether the initialization is normal. |
| 20482 | During playback, the client tried to interrupt and play back the next one but failed (which should succeed normally). | Check whether the code logic is correct. |
| 20483 | Parameter is empty. | Check whether the API parameters in the code are correct. |
| 20484 | Internal error. | An error occurred while initializing the player. This error code is generally caused by failure in decoding, and the error should be located with the aid of logs. |

#### Sample code

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
		switch (eventType) {
			case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
			{
			// Process
			break;
				}
			...
					case ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE:
			{
			// Process
			break;
			}
		}
}
```



### Stopping audio playback

This API is used to stop audio playback. There will be a callback for playback completion when the playback stops.

#### Function prototype  

```
ITMGPTT virtual int StopPlayFile()
```

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->StopPlayFile();
```



### Getting audio file size

This API is used to get the size of an audio file.

#### Function prototype  

```
ITMGPTT virtual int GetFileSize(const char* filePath)
```

| Parameter | Type | Description |
| -------- | :----: | -------------- |
| filePath | char* | Path of audio file, which is a local path. |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetFileSize(filePath);

```

### Getting audio file duration

This API is used to get the duration of an audio file in milliseconds.

#### Function prototype  

```
ITMGPTT virtual int GetVoiceFileDuration(const char* filePath)
```

| Parameter | Type | Description |
| -------- | :----: | -------------- |
| filePath | char* | Path of audio file, which is a local path. |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->GetVoiceFileDuration(filePath);
```


## Voice Message Upload and Download

### Uploading audio file

This API is used to upload an audio file.

#### Function prototype  

```
ITMGPTT virtual int UploadRecordedFile(const char* filePath)
```

| Parameter | Type | Description |
| -------- | :----: | -------------- |
| filePath | char* | Path of uploaded audio file, which is a local path |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->UploadRecordedFile(filePath);
```

### Callback for audio file upload completion

After the audio file is uploaded, the event message `ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path`, and `file_id`.

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ------------------------------ | ------------------------------------------------------ |
| 8193 | An error occurred while accessing the file during upload. | Ensure the existence of the file and the validity of the file path. |
| 8194 | Signature verification failed. | Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized. |
| 8195 | A network error occurred. | Check whether the device can access the internet. |
| 8196 | The network failed while getting the upload parameters. | Check whether the authentication is correct and whether the device can access the internet. |
| 8197 | The packet returned during the process of getting the upload parameters is empty. | Check whether the authentication is correct and whether the device network can normally access the internet. |
| 8198 | Failed to decode the packet returned during the process of getting the upload parameters. | Check whether the authentication is correct and whether the device can access the internet. |
| 8200 | No `appinfo` is set. | Check whether the `apply` API is called or whether the input parameters are empty. |

#### Sample code

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
		switch (eventType) {
			case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
			{
			// Process
			break;
				}
			...
					case ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE:
			{
			// Process
			break;
			}
		}
}
```

### Downloading the audio file

This API is used to download an audio file.

#### Function prototype  

```
ITMGPTT virtual int DownloadRecordedFile(const char* fileId, const char* filePath) 
```

| Parameter | Type | Description |
| ---------------- | :----: | ------------------------------------- |
| fileId | char* | URL path of file |
| filePath | char* | Local path of saved file |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->DownloadRecordedFile(fileID,filePath);
```

### Callback for audio file download completion

After the audio file is downloaded, the event message `ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE` will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path`, and `file_id`.

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| 12289 | An error occurred while accessing the file during download. | Check whether the file path is valid. |
| 12290 | Signature verification failed. | Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized. |
| 12291 | Network storage system exception | The server failed to get the audio file. Check whether the API parameter `fileid` is correct, whether the network is normal, and whether the file exists in COS. |
| 12292 | Server file system error. | Check whether the device can access the internet and whether the file exists on the server. |
| 12293 | The HTTP network failed during the process of getting the download parameters. | Check whether the device can access the internet. |
| 12294 | The packet returned during the process of getting the download parameters is empty. | Check whether the device can access the internet. |
| 12295 | Failed to decode the packet returned during the process of getting the download parameters. | Check whether the device can access the internet. |
| 12297 | No `appinfo` is set. | Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized. |


#### Sample code

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
		switch (eventType) {
			case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
			{
			// Process
			break;
				}
			...
					case ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE:
			{
			// Process
			break;
			}
		}
}
```


## Speech-to-Text Service




### Converting audio file to text

This API is used to convert a specified audio file to text.

#### Function prototype  

```
ITMGPTT virtual void SpeechToText(const char* fileID)
```

| Parameter | Type | Description |
| ------ | :----: | ---------------------------------- |
| fileID | char* | URL of audio file |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SpeechToText(fileID);
```



### Translating audio file into text in specified language

This API can specify a language for recognition or translate the information recognized in speech into a specified language and return the translation.

#### Function prototype  

```
ITMGPTT virtual int SpeechToText(const char* fileID,const char* speechLanguage,const char* translateLanguage)
```
| Parameter | Type | Description |
| ------------- |:-------------:|-------------|
| fileID | char* | URL of audio file, which will be retained on the server for 90 days |
| speechLanguage | char* | The language in which the audio file is to be converted to text. For parameters, please see [ Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260) |
| translatelanguage | char* | The language into which the audio file will be translated. For parameters, please see [Language Parameter Reference List](https://intl.cloud.tencent.com/document/product/607/30260). This parameter is currently unavailable. Enter the same value as that of `speechLanguage`. |

#### Sample code  

```
ITMGContextGetInstance()->GetPTT()->SpeechToText(filePath,"cmn-Hans-CN","cmn-Hans-CN");
```



### Callback for recognition

After the specified audio file is converted to text, the event message ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE will be returned, which will be identified in the `OnEvent` function.
The passed parameters include `result`, `file_path` and `text` (recognized text).

#### Error codes

| Error Code Value | Cause | Suggested Solution |
| -------- | ---------------------- | ------------------------------------------------------------ |
| 32769 | An internal error occurred. | Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |
| 32770 | Network failed. | Check whether the device can access the internet. |
| 32772 | Failed to decode the returned packet. | Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |
| 32774 | No `appinfo` is set. | Check whether the authentication key is correct and whether the voice messaging and speech-to-text feature is initialized. |
| 32776 | `authbuffer` check failed. | Check whether `authbuffer` is correct. |
| 32784 | Incorrect speech-to-text conversion parameter. | Check whether the API parameter `fileid` in the code is empty. |
| 32785 | Speech-to-text translation returned an error. | Error with the backend of voice messaging and speech-to-text feature. Analyze logs, get the actual error code returned from the backend to the client, and ask backend personnel for assistance. |

#### Sample code

```
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
		switch (eventType) {
			case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
			{
			// Process
			break;
				}
			...
					case ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE:
			{
			// Process
			break;
			}
		}
}
```



## Advanced APIs

### Getting diagnostic messages
This API is used to get information on the quality of real-time audio/video calls, which is mainly used to view real-time call quality and troubleshoot problems and can be ignored on the business side.

#### Function prototype
```
ITMGRoom virtual const char* GetQualityTips()
```
#### Sample code  
```
ITMGContextGetInstance()->GetRoom()->GetQualityTips();
```


### Getting version number
#### Function prototype

```
ITMGContext virtual const char* GetSDKVersion()
```



#### Sample code  

```
ITMGContextGetInstance()->GetSDKVersion();
```



### Setting log printing level

This API is used to set the level of logs to be printed. It is recommended to keep the default level.

#### Function prototype

```
ITMGContext int SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | Sets the level of logs to be written. `TMG_LOG_LEVEL_NONE` indicates not to write. Default value: TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | Sets the level of logs to be printed. `TMG_LOG_LEVEL_NONE` indicates not to print. Default value: TMG_LOG_LEVEL_ERROR |



| ITMG_LOG_LEVEL | Description |
| ----------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE=0 | Does not print logs |
| TMG_LOG_LEVEL_ERROR=1 | Prints error logs (default) |
| TMG_LOG_LEVEL_INFO=2 | Prints info logs |
| TMG_LOG_LEVEL_DEBUG=3 | Prints debug logs |
| TMG_LOG_LEVEL_VERBOSE=4 | Prints verbose logs |

#### Sample code  

```
ITMGContext* context = ITMGContextGetInstance();
context->SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);
```



### Setting log printing path
This API is used to set the log printing path.
The default path is `%appdata%\Tencent\GME\ProcessName|`.


#### Function prototype

```
ITMGContext virtual int SetLogPath(const char* logDir) 
```

| Parameter | Type | Description |
| ------ | :----: | ---- |
| logDir | char* | Path |

#### Sample code  

```
cosnt char* logDir = ""// Set a path by yourself

ITMGContext* context = ITMGContextGetInstance();
context->SetLogPath(logDir);
```

### Blocking audio data

This API is used to add an ID to the audio data blocklist. This operation blocks audio from someone and only applies to the local device. A returned value of `0` indicates the call is successful. Assume that users A, B, and C are all speaking using their mic in a room: 
- If A blocks C, A can only hear B;
- If B blocks neither A nor C, B can hear both of them;
- If C blocks neither A nor B, C can hear both of them.


#### Function prototype  

```
ITMGContext ITMGAudioCtrl int AddAudioBlackList(const char* openId)
```

| Parameter | Type | Description |
| ------ | :----: | ----------------- |
| openId | char* | ID to be blocked |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->AddAudioBlackList(openId);
```

### Unblocking audio data

This API is used to remove an ID from the audio data blocklist. A returned value of `0` indicates the call is successful.

#### Function prototype  

```
ITMGContext ITMGAudioCtrl int RemoveAudioBlackList(const char* openId)
```

| Parameter | Type | Description |
| ------ | :----: | ----------------- |
| openId | char* | ID to be unblocked |

#### Sample code  

```
ITMGContextGetInstance()->GetAudioCtrl()->RemoveAudioBlackList(openId);
```

## Callback Messages

### Message list

| Message | Description |   
| ------------- |:-------------:|
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM | Indicates that a member enters an audio room. |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | Indicates that a member exits an audio room. |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | Indicates that a room is disconnected for network or other reasons. |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | Indicates a room type change event. |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE | Indicates that a new mic is added |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE | Indicates that a mic is lost |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE | Indicates that a new speaker is added |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE | Indicates that a speaker is lost |
| ITMG_MAIN_EVENT_TYPE_ACCOMPANY_FINISH | Indicates that the accompaniment is over. |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | Indicates that the room members are updated. |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_USERS_UPDATE | Indicates that the room member quantity is updated. |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_AUDIOSTREAMS_UPDATE | Indicates that the room audio stream quantity is updated. |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY | Indicates the room quality information. |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE | Indicates that PTT recording is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE | Indicates that PTT upload is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE | Indicates that PTT download is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE | Indicates that PTT playback is completed. |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE | Indicates that speech-to-text conversion is completed. |

### Data list

| Message | Data | Sample |
| ------------- |:-------------:|------------- |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM | result; error_info | {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_EXIT_ROOM | result; error_info | {"error_info":"","result":0} |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info | {"error_info":"waiting timeout, please check your network","result":0} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_TYPE | result; error_info; sub_event_type; new_room_type | {"error_info":"","new_room_type":0,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_NEW_DEVICE | result; error_info | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_SPEAKER_LOST_DEVICE | result; error_info | {"deviceID":"{0.0.0.00000000}.{a4f1e8be-49fa-43e2-b8cf-dd00542b47ae}","deviceName":"Speaker (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":false,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_NEW_DEVICE | result; error_info | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":true,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVENT_TYPE_MIC_LOST_DEVICE | result; error_info | {"deviceID":"{0.0.1.00000000}.{5fdf1a5b-f42d-4ab2-890a-7e454093f229}","deviceName":"Mic (Realtek High Definition Audio)","error_info":"","isNewDevice":false,"isUsedDevice":true,"result":0} |
| ITMG_MAIN_EVNET_TYPE_USER_UPDATE | user_list;  event_id | {"event_id":1,"user_list":["0"]} |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_USERS_UPDATE | AllUser; AccUser; ProxyUser | {"AllUser":3,"AccUser":2,"ProxyUser":1} |
| ITMG_MAIN_EVENT_TYPE_NUMBER_OF_AUDIOSTREAMS_UPDATE | AudioStreams | {"AudioStreams":3} |
| ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY | weight; loss; delay | {"weight":5,"loss":0.1,"delay":1} |
| ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE | result; file_path | {"file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_UPLOAD_COMPLETE | result; file_path;file_id | {"file_id":"","file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_DOWNLOAD_COMPLETE | result; file_path;file_id | {"file_id":"","file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_PLAY_COMPLETE | result; file_path | {"file_path":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_SPEECH2TEXT_COMPLETE | result; text;file_id | {"file_id":"","text":"","result":0} |
| ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE | result; file_path; text;file_id | {"file_id":"","file_path":","text":"","result":0} |
