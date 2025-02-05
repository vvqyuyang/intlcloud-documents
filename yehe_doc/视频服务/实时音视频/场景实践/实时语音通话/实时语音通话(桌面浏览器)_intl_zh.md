本文介绍如何实现一套可以在浏览器上运行的语音通话解决方案，文章分成两个部分：
- 第一部分：介绍如何开通服务并跑通我们提供的演示 Demo。
- 第二部分：介绍如何使用 TRTCCalling 组件快速搭建自己的语音通话功能。

## 环境要求
请使用最新版本的 Chrome 浏览器。目前桌面端 Chrome 浏览器支持 TRTC 桌面浏览器 SDK 的相关特性比较完整，因此建议使用 Chrome 浏览器进行体验。

TRTCCalling 依赖以下端口进行数据传输，请将其加入防火墙白名单，配置完成后，您可以通过访问并体验 [官网 Demo](https://demo-1252463788.cos.ap-shanghai.myqcloud.com/trtccalling/demo/index.html) 检查配置是否生效。
  - TCP 端口：8687
  - UDP 端口：8000，8080，8800，843，443，16285
  - 域名：qcloud.rtc.qq.com

目前该方案支持如下平台：

| 操作系统 |          浏览器类型          | 浏览器最低版本要求 |
| :------: | :--------------------------: | :----------------: |
|  Mac OS  |     桌面版 Safari 浏览器     |        11+         |
|  Mac OS  |     桌面版 Chrome 浏览器     |        56+         |
|  Mac OS  |    桌面版 Firefox 浏览器     |        56+         |
|  Mac OS  |      桌面版 Edge 浏览器      |        80+         |
| Windows  |     桌面版 Chrome 浏览器     |        56+         |
| Windows  | 桌面版 QQ 浏览器（极速内核） |       10.4+        |
| Windows  |    桌面版 Firefox 浏览器     |        56+         |
| Windows  |      桌面版 Edge 浏览器      |        80+         |

## 跑通测试 Demo

[](id:step1)
### 步骤1：创建新的应用
1. [注册腾讯云](https://intl.cloud.tencent.com/document/product/378/17985) 账号，并完成 实名认证，未进行实名认证的用户无法购买中国大陆的实时视频通话实例。
2. 登录实时音视频控制台，选择【开发辅助】>【[快速跑通Demo](https://console.cloud.tencent.com/trtc/quickstart)】。
3. 输入应用名称，例如 `TestTRTC` ，单击【创建】。

[](id:step2)
### 步骤2：下载 SDK 和 Demo 源码
1. 根据实际业务需求下载 SDK 及配套的 Demo 源码。
2. 下载完成后，单击【已下载，下一步】。

[](id:step3)
### 步骤3：配置 Demo 工程文件
1. 进入修改配置页，根据您下载的源码包，选择相应的开发环境。
2. 找到并打开 `Web/TRTCScenesDemo/trtc-calling-web/public/debug/GenerateTestUserSig.js` 文件。
3. 设置 `GenerateTestUserSig.js` 文件中的相关参数：
<ul style="margin:0"><li/>SDKAPPID：默认为0，请设置为实际的 SDKAppID。
<li/>SECRETKEY：默认为空字符串，请设置为实际的密钥信息。</ul>
4. 粘贴完成后，单击【已复制粘贴，下一步】即创建成功。
5. 编译完成后，单击【回到控制台概览】即可。


>!
>- 本文提到的生成 UserSig 的方案是在客户端代码中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此 **该方法仅适合本地跑通 Demo 和功能调试**。
>- 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/647/35166)。

[](id:step4)
### 步骤4：运行 Demo
1. 在 npm 命令行窗口中依次输入如下命令：
```
npm install
npm run serve
```
2. 启动 Chrome 浏览器中打开链接 `http://localhost:8080/` ，如果一切正常，Demo 运行界面如图所示：
3. 输入用户 userid，单击【登录】，并选择【语音通话】：
4. 输入呼叫用户 userid，单击【呼叫】：
5. 即可进行语音通话：


## 搭建自己的语音通话
### 步骤1：集成 TRTCCalling 组件
>?
>- 从v0.6.0起，需要手动安装依赖 [trtc-js-sdk](https://www.npmjs.com/package/trtc-js-sdk) 和 [tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk) 以及 [tsignaling](https://www.npmjs.com/package/tsignaling)。
>- 为了减小 trtc-calling-js.js 的体积，避免和接入侧已使用的 trtc-js-sdk 和 tim-js-sdk 以及 tsignaling 发生版本冲突，trtc-js-sdk 和 tim-js-sdk 以及 tsignaling 不再被打包到 trtc-calling-js.js，在使用前您需要手动安装依赖。

```javascript
  npm i trtc-js-sdk --save
  npm i tim-js-sdk --save
  npm i tsignaling --save
  npm i trtc-calling-js --save



  //如果您通过 script 方式使用 trtc-calling-js，需要按顺序先手动引入 trtc.js
  <script src="./trtc.js"></script>
  
  // 接着手动引入 tim-js.js
  <script src="./tim-js.js"></script>
  
  // 然后再手动引入 tsignaling.js
  <script src="./tsignaling.js"></script>



  // 最后再手动引入 trtc-calling-js.js
  <script src="./trtc-calling-js.js"></script>
```
### 步骤2：创建 TRTCCalling 对象
创建 TRTCCalling 对象，并将 SDKAppID 参数设置为您自己的 SDKAppID。
```javascript
import TRTCCalling from 'trtc-calling-js';


let options = {
  SDKAppID: 0 // 接入时需要将0替换为您的 SDKAppID
};
const trtcCalling = new TRTCCalling(options);
```

### 步骤3：完成登录
```javascript
trtcCalling.login({
  userID,
  userSig,
});
```

### 步骤4：实现 1v1 通话
#### 主叫方：呼叫某个用户
```javascript
trtcCalling.call({
  userID,  //用户 ID
  type: 2, //通话类型，0-未知， 1-语音通话，2-视频通话
  timeout  //邀请超时时间, 单位 s(秒)
});
```

#### 被叫方：接听新的呼叫
```javascript
// 接听
trtcCalling.accept({
  inviteID, //邀请 ID, 标识一次邀请
  roomID,   //通话房间号 ID
  callType  //0-未知， 1-语音通话，2-视频通话
});
//拒绝
trtcCalling.reject({ 
  inviteID, //邀请 ID, 标识一次邀请
  isBusy //是否是忙线中， 0-未知， 1-语音通话，2-视频通话
  })
```

#### 挂断
```javascript
trtcCalling.hangup()
```
