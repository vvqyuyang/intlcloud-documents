## 효과
Demo를 [다운로드](https://intl.cloud.tencent.com/document/product/647/35076) 및 설치하여 화면 공유, 뷰티 필터, 저 딜레이 회의 등 TRTC 다중 사용자 화상 회의 시나리오 관련 기능을 체험해 볼 수 있습니다.

<table>
     <tr>
         <th>회의 입장</th>  
         <th>화면 공유</th>  
     </tr>
<tr>
</tr>
</table>

빠른 다중 사용자 화상 회의 기능 연결을 위해 직접 Tencent Cloud에서 제공하는 Demo를 기반으로 적합하게 수정하거나, TRTCMeeting 모듈을 사용해 UI 인터페이스를 사용자 정의할 수도 있습니다.

## Demo UI 인터페이스 재사용

### 1단계: 신규 애플리케이션 생성

1. TRTC 콘솔에 로그인하여 [개발 보조]>[빠른 Demo 활성화](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 이름(예: `TestMeetingRoom`)을 입력한 후 [애플리케이션 생성]을 클릭합니다.

>? 해당 기능은 Tencent Cloud의 [TRTC](https://intl.cloud.tencent.com/document/product/647/35078)와 [IM](https://intl.cloud.tencent.com/document/product/1047) 두 서비스 기반의 PAAS 서비스를 이용합니다. 따라서 TRTC를 활성화한 후 IM 서비스도 함께 활성화해야 합니다. IM은 부가 서비스이며, 자세한 과금 규정은 [IM 가격 설명](https://intl.cloud.tencent.com/document/product/1047/34350)을 참조하십시오.



### 2단계: SDK와 Demo 소스 코드 다운로드
1. 커서를 해당하는 부분으로 이동한 후, [Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)를 클릭하여 Github(또는 [ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip) 클릭)로 이동하여 SDK와 Demo 소스 코드를 다운로드합니다.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. 다운로드 완료 후 TRTC 콘솔로 돌아가 [다운로드 완료, 다음 단계]를 클릭하면 SDKAppID와 키 정보를 확인할 수 있습니다.

### 3단계: Demo 프로젝트 파일 설정
1. [2단계](#ui.step2)에서 다운로드한 소스 패키지를 압축 해제합니다.
2. `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.h` 파일에서 관련 매개변수를 설정합니다.
  <ul><li>SDKAPPID: 0으로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.</li>
  <li>SECRETKEY: 공백으로 기본 설정되어 있으며 실제 키 정보로 설정하십시오.</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. TRTC 콘솔로 돌아가 [붙여넣기 완료, 다음 단계]를 클릭합니다.
5. [가이드 닫기, 콘솔 관리 애플리케이션 열기]를 클릭합니다.

>!
>!본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 방법입니다. 여기에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 귀하의 서버에 통합하고 App 지향의 인터페이스를 제공합니다. UserSig가 필요한 경우 귀하의 App이 비즈니스 서버에 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

### 4단계: Demo 실행
Xcode(11.0 버전 이상)를 사용하여 오픈 소스 프로그램인 `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`를 열고 [실행]을 클릭하면 해당 Demo가 디버깅됩니다.

### 5단계: Demo 소스 코드 수정
소스 코드 ``trtcmeetingdemo``에는 ui 폴더와 model 폴더가 포함되어 있으며, ui 폴더 의 모든 파일은 인터페이스 관련 코드입니다. 2차 수정을 위해 하기와 같이 해당 파일 또는 폴더에 해당하는 UI 화면에 대한 설명을 제공합니다.

| 파일 또는 폴더 | 기능 설명 |
|:-------:|:--------|
| SegmentVC | 인터페이스 설정 관련 UI 구현 코드 |
| TRTCBroadcastExtensionLauncher.swift | 녹화 팝업창 관련 UI 구현 코드 |
| TRTCMeetingNewViewController | 화상 회의 생성 인터페이스 UI 구현 코드 |
| TRTCMeetingMainViewController | 회의 방 인터페이스 UI 구현 코드 |
| TRTCMeetingMemberViewController | 참여자 리스트 인터페이스 UI 구현 코드 |
| TRTCMeetingMoreViewController | 인터페이스 설정 관련 UI 구현 코드  |


<span id="model"> </span>
## 사용자 정의 UI 인터페이스 구현

[소스 코드](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCMeetingDemo)의 trtcmeetingdemo 폴더에는 ui 폴더와 model 폴더가 포함되어 있으며, model 폴더에는 재사용 가능한 오픈 소스 모듈인 TRTCMeeting이 포함되어 있습니다. `TRTCMeeting.h` 파일에서 해당 모듈에서 제공하는 액세스 함수를 확인할 수 있으며 해당 액세스를 사용해 사용자 정의 UI 인터페이스를 구현할 수 있습니다.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)


<span id="model.step1"> </span>
### 1단계: SDK 통합
다중 사용자 화상 회의 모듈 TRTCMeeting은 TRTC SDK와 IM SDK에 종속되어 있습니다. 다음 순서에 따라 해당 두 SDK를 프로젝트에 통합할 수 있습니다.

**방법1: cocoapods 웨어하우스를 통한 종속 **
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?해당 두 SDK 제품의 최신 버전은 [TRTC](https://github.com/tencentyun/TRTCSDK)와 [IM](https://github.com/tencentyun/TIMSDK) Github 메인 페이지에서 다운로드할 수 있습니다.

**방법2: 로컬을 통한 종속**
cocoapods 웨어하우스 연결이 비교적 느린 개발 환경인 경우, 직접 ZIP 패키지를 다운로드하고 통합 가이드 문서를 참조하여 프로젝트에 통합할 수 있습니다.

| SDK | 다운로드 페이지 | 통합 가이드 |
|---------|---------|---------|
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [통합 가이드 문서](https://intl.cloud.tencent.com/document/product/1047/34306) |

<span id="model.step2"> </span>
### 2단계: 권한 설정
info.plist 파일에 Privacy > Camera Usage Description, Privacy > Microphone Usage Description을 추가하여 카메라와 마이크 권한을 요청해야 합니다.

<span id="model.step3"> </span>
### 3단계: TRTCMeeting 모듈 가져오기
`iOS/LiteAVDemo/TXLiteAVDemo/TRTCMeetingDemo/model` 디렉터리의 모든 파일을 프로젝트에 붙여넣습니다.

<span id="model.step4"> </span>
### 4단계: 모듈 생성 및 로그인
1. `sharedInstance` 인터페이스를 호출하여 TRTCMeeting 모듈의 인스턴스 객체를 생성합니다.
2. `setDelegate` 함수를 호출하여 모듈의 이벤트 알림을 등록합니다.
3. `login` 함수를 호출해 모듈에 로그인하고, 다음 표를 참고하여 관련 매개변수를 입력합니다.
<table> 
<tr>
<th>매개변수 이름</th>
<th>작용</th>
</tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTC 콘솔</a>에서 SDKAppID를 확인할 수 있습니다.</td>
</tr><tr>
<td>userId</td>
<td>현재 사용자 ID이며, 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시부호(-), 언더바(_)만 허용됩니다.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud가 설계한 일종의 보안 서명으로, 취득 방법은 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig 계산 방법</a>을 참조하십시오.</td>
</tr><tr>
<td>callback</td>
<td>로그인 콜백이며, 성공 시 code는 0입니다.</td>
</tr>
</table>

```swift
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)

TRTCMeeting.sharedInstance().login(SDKAPPID, userId: userID, userSig: userSig, callback: { code, message in
    if code == 0 {
        //로그인 성공
    }
})
```

<span id="model.step5"> </span>
### 5단계: 다중 사용자 회의 생성
1. 주최자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 주최자는 `setDelegate`를 호출하여 `createMeeting` 이벤트를 호출하여 새로운 회의 방을 생성할 수 있습니다.
3. 주최자는 `startCameraPreview`를 호출하여 비디오 화면 수집을 시작하고 `startMicrophone`를 호출하여 오디오 수집을 시작할 수 있습니다.
4. 주최자가 뷰티 필터 사용을 원할 경우 인터페이스에 뷰티 필터 조절 버튼을 설정해 호출하고 `getBeautyManager`를 통해 뷰티 필터를 설정할 수 있습니다.
>?엔터프라이즈 버전 이외의 SDK는 얼굴 변경 및 스티커 효과 기능을 지원하지 않습니다.

![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```swift
// 1. 호스트 닉네임 및 프로필 사진 설정
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. 호스트 방 생성
trtcMeeting.createMeeting(roomId) { (code, msg) in
 if code == 0 {
   // 방 생성 성공
  let localPreviewView=getRenderView(userId: selfUserId)!
  TRTCMeeting.sharedInstance().startCameraPreview(true, view: localPreviewView)
  TRTCMeeting.sharedInstance().startMicrophone();
  
  // 기본 뷰티 필터 매개변수 사용
  beautyPannel.resetAndApplyValues()
  return;
 }
}
```

<span id="model.step6"> </span>
### 6단계: 다중 사용자 회의 방에 참여자 입장
1. 참여자는 [4단계](#model.step4) 로그인 실행 후 `setSelfProfile`을 호출하여 자신의 닉네임과 프로필 사진을 설정할 수 있습니다.
2. 참여자는 `enterMeeting`을 호출하고 회의 방 번호를 전달하여 회의 방에 입장할 수 있습니다.
3. 참여자는 `startCameraPreview`를 호출하여 비디오 화면 수집을 시작하고 `startMicrophone`를 호출하여 오디오 수집을 시작할 수 있습니다.
4. 다른 참여자가 카메라를 켜면 `onUserVideoAvailable` 이벤트가 수신됩니다. 이때 `startRemoteView`를 호출하고 userId를 전달하면 재생이 시작됩니다.

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```swift
// 1. 참여자 닉네임 및 프로필 사진 설정
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2.enterMeeting 함수 구현
trtcMeeting.enterMeeting(roomId) { (code, msg) in
   if code == 0{
     trtcMeeting.startCameraPreview(true, view: localPreviewView)
     trtcMeeting.startMicrophone()
   } else {
      self.view.makeToast("회의 입장 실패:" + msg!)
   }
}
```

```swift
let renderView = getRenderView(userId: userId)
if available && renderView != nil {
  //콜백을 수신하고 startRemoteView를 호출하여 userId를 전달해 재생을 시작합니다.
  TRTCMeeting.sharedInstance().startRemoteView(userId, view: renderView!) { (code, message) in
   debugPrint("startRemoteView" + "\(code)" + message!)
  }
} else {
 TRTCMeeting.sharedInstance().stopRemoteView(userId) { (code, message) in
   debugPrint("stopRemoteView" + "\(code)" + message!)
  }
}
//현재 인터페이스 새로고침
renderView?.refreshVideo(isVideoAvailable: available)
```

<span id="model.step7"> </span>
### 7단계: 화면 공유
1. `startScreenCapture`를 호출하여 인코딩 매개변수와 녹화 팝업창을 전달하면 화면 공유 기능을 구현할 수 있습니다. 자세한 정보는 [TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)를 참조하십시오.
2. 회의 중 다른 참여자들은 `onUserVideoAvailable` 이벤트 알림을 수신합니다.

>!화면 공유 및 카메라 수집은 상호 충돌되는 작업입니다. 화면 공유 기능을 활성화 하고 싶은 경우, 먼저 `stopCameraPreview`를 호출하여 카메라 수집을 비활성화해야 합니다.

```swift
// 1. 버튼을 클릭하여 화면 공유 활성화
if #available(iOS 12.0, *) {
  // 녹화 전에는 반드시 먼저 카메라 수집을 비활성화해야 합니다.
  self.setLocalVideo(isVideoAvailable: false)
  
  // 화면 공유
  let params = TRTCVideoEncParam()
  params.videoResolution = TRTCVideoResolution._1280_720
  params.videoFps = 10
  params.videoBitrate = 1800
  TRTCMeeting.sharedInstance().startScreenCapture(params)
  TRTCBroadcastExtensionLauncher.launch()
} else {
  self.view.makeToast("시스템 버전이 12.0 이하입니다. 시스템을 업데이트하십시오.")
}     
```

<span id="model.step8"> </span>
### 8단계: 텍스트 채팅 및 금지어 메시지 구현
- `sendRoomTextMsg`를 통해 일반 텍스트 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomTextMsg` 콜백을 수신하게 됩니다.
IM의 백그라운드에는 기본적으로 민감 단어 필터링 규칙이 있으며, 민감 단어가 포함된 텍스트 메시지로 판단될 경우 전달되지 않습니다.

```swift
// 발신 측: 텍스트 메시지 발송
TRTCMeeting.sharedInstance().sendRoomTextMsg("Hello Word!") { (code, message) in
  debugPrint("send result: ", code)
}

// 수신 측: 텍스트 메시지 리슨
func onRecvRoomTextMsg(_ message: String?, userInfo: TRTCMeetingUserInfo) {
  debugPrint(":\(String(describing: userInfo.userId))님이 발송한 메시지:\(String(describing: message))")
}
```

- `sendRoomCustomMsg`를 통해 사용자 정의(신호) 메시지를 발송할 수 있으며, 해당 방에 있는 모든 호스트와 시청자가 `onRecvRoomCustomMsg` 콜백을 수신하게 됩니다.
사용자 정의 메시지는 주로 금지어 사용 제한 등과 같은 사용자 정의 신호 전송에 사용됩니다.

```swift
// 발신 측: 사용자 정의 Cmd를 통해 금지어 알림을 구분할 수 있습니다.
// eg:"CMD_MUTE_AUDIO" 금지어 알림
TRTCMeeting.sharedInstance().sendRoomCustomMsg("CMD_MUTE_AUDIO", message: "1") { (code, message) in
  debugPrint("send result: ", code)
}

// 수신 측: 사용자 정의 메시지 리슨
func onRecvRoomCustomMsg(_ cmd: String?, message: String?, userInfo: TRTCMeetingUserInfo) {
  if cmd == "CMD_MUTE_AUDIO" {
    debugPrint(":\(String(describing: userInfo.userId))님이 발송한 금지어 알림:\(String(describing: message))")
    TRTCMeeting.sharedInstance().muteLocalAudio(message == "1")
  }
}
```
