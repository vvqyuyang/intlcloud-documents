## 操作场景	
为方便 Unity 开发者调试和接入腾讯云游戏多媒体引擎产品 API，本文主要为您介绍适用于 Unity 开发的快速接入文档。		
		
GME 快速入门文档只提供最主要的接入接口，更多详细接口请参见 [相关接口文档](https://intl.cloud.tencent.com/document/product/607/15228)。
			
|重要接口     | 接口含义|
| ------------- |:-------------:|
|Init    		|初始化 GME 	|
|Poll    		|触发事件回调	|
|EnterRoom	 	|进房  		|
|EnableMic	 	|开麦克风 	|
|EnableSpeaker		|开扬声器 	|

>
>- GME 使用前请对工程进行配置，否则 SDK 不生效。
>- GME 的接口调用成功后返回值为 QAVError.OK，数值为0。
>- GME 的接口调用要在同一个线程下。
>- GME 需要周期性的调用 Poll 接口触发事件回调。
>- GME 回调信息参考回调消息列表。
>- 设备的操作要在进房成功之后。
>- 错误码详情可参考 [错误码](https://intl.cloud.tencent.com/document/product/607/15173)。

## 接入步骤
### 1. 初始化 SDK

参数获取请参见 [接入指引](https://intl.cloud.tencent.com/document/product/607/39698)。

此接口需要来自腾讯云控制台的 SDKAppID 号码作为参数，再加上 openID，这个 openID 是唯一标识一个用户，规则由 App 开发者自行制定，App 内不重复即可（目前只支持 INT64）。
>初始化 SDK 之后才可以进房。
####  函数原型

```
ITMGContext Init(string sdkAppID, string openID)
```

|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| sdkAppId    	|String  |来自腾讯云控制台的 AppId 号码。				|
| openID    		|String  |OpenID 只支持 Int64 类型（转为 string 传入），必须大于10000，用于标识用户。|

####  示例代码 

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
//通过返回值判断是否初始化成功
if (ret != QAVError.OK)
    {
        Debug.Log("SDK初始化失败:"+ret);
        return;
    }
```

### 2. 触发事件回调
通过在 update 里面周期的调用 Poll 可以触发事件回调。GME 需要周期性的调用 Poll 接口触发事件回调。
####  函数原型

```
ITMGContext public abstract int Poll();
```
####  示例代码 

```
public void Update()
    {
        ITMGContext.GetInstance().Poll();
    }
```

### 3. 鉴权信息
生成 AuthBuffer，用于相关功能的加密和鉴权。  

>离线语音获取鉴权时，房间号参数必须填 null。

#### 函数原型
```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| appId    		|int   		|来自腾讯云控制台的 AppId 号码。		|
| roomId    		|string   		|房间号，最大支持127字符（离线语音房间号参数必须填 null）。|
| openId    	|string 	|用户标识。与 Init 时候的 openID 相同。					|
| key    		|string 	|来自腾讯云 [控制台](https://console.cloud.tencent.com/gamegme) 的权限密钥。				|



####  示例代码  
```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}
```

### 4. 加入房间
用生成的鉴权信息进房。加入房间默认不打开麦克风及扬声器。

####  函数原型
```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)
```
|参数     | 类型         |含义|
| ------------- |:-------------:|-------------|
| roomId		|string    	|房间号，最大支持127字符。					|
| roomType 	|ITMGRoomType		|房间音频类型。		|
| authBuffer 	|Byte[] 	|鉴权码。					|

房间音频类型请参考 [音质选择](https://intl.cloud.tencent.com/document/product/607/18522)。


####  示例代码  
```
ITMGContext.GetInstance().EnterRoom(strRoomId, ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);
```

### 5. 加入房间事件的回调
加入房间后，需要通过委托函数进行回调。其中包含两个信息：result 及 error_info。
#### 函数原型
```
委托函数：
public delegate void QAVEnterRoomComplete(int result, string error_info);
事件函数：
public abstract event QAVEnterRoomComplete OnEnterRoomCompleteEvent;
```

####  示例代码  
```
对事件进行监听：
ITMGContext.GetInstance().OnEnterRoomCompleteEvent += new QAVEnterRoomComplete(OnEnterRoomComplete);

监听处理：
void OnEnterRoomComplete(int err, string errInfo)
    {
	if (err != 0) {
  			ShowLoginPanel("错误码:" + err + " 错误信息:" + errInfo);
            return;
	}else{
		//进房成功
    }
}
```


### 6. 开启关闭麦克风
此接口用来开启关闭麦克风。加入房间默认不打开麦克风及扬声器。

>
>- 导出各平台可执行文件时，请确保工程中已申请开启麦克风权限，及使用过程中麦克风权限已开启。
>- 移动端可以使用 CheckMicPermission 此接口进行麦克风权限判断。

####  函数原型  
```
ITMGAudioCtrl EnableMic(bool isEnabled)
```
|参数     | 类型         |意义|
| ------------- |:-------------:|-------------|
| isEnabled    |boolean     |如果需要打开麦克风，则传入的参数为 true，如果关闭麦克风，则参数为 false。|

####  示例代码  
```
//打开麦克风
ITMGContext.GetInstance().GetAudioCtrl().EnableMic(true);
```


### 7. 开启关闭扬声器
此接口用于开启关闭扬声器。
####  函数原型  
```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```
|参数     | 类型         |意义|
| ------------- |:-------------:|-------------|
| isEnabled    |bool        |如果需要关闭扬声器，则传入的参数为 false，如果打开扬声器，则参数为 true。|

####  示例代码  
```
//打开扬声器
ITMGContext.GetInstance().GetAudioCtrl().EnableSpeaker(true);
```
