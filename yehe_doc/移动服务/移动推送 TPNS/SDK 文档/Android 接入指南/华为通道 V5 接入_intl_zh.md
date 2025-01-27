## 操作场景


移动推送 TPNS 跟进各厂商通道推送服务的更新进度，提供集成华为推送 HMS Core Push SDK 的插件依赖包供用户选择使用。

> !  
> - 华为推送只有在签名发布包环境下，才可注册厂商通道成功并通过厂商通道进行推送。
> - 华为通道不支持抵达回调，支持点击回调。

## 在华为推送平台配置应用

### 获取密钥

1. 进入 [华为开放平台](http://developer.huawei.com)。
2. 注册和登录开发者账号，详情参见 [账号注册认证](https://developer.huawei.com/consumer/cn/devservice/doc/20300)（如果您是新注册账号，需进行实名认证）。
3. 在华为推送平台中新建应用，详情参见 [创建应用](https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-create_app)（应用包名需跟您在移动推送 TPNS 平台填写的一致）。
4. 获取并复制应用的 AppID 和 AppSecret，填入 【[移动推送 TPNS 控制台](https://console.cloud.tencent.com/tpns)】>【配置管理】>【基础配置】>【华为官方推送通道】栏目中。


### 配置 SHA256 证书指纹

获取 SHA256 证书指纹，并在华为推送平台中配置证书指纹，参见 [生成签名证书指纹](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/Preparations#generate_finger)。

### 获取华为推送配置文件

登录华为开放平台，进入【我的项目】> 选择项目 > 【项目设置】，下载华为应用最新配置文件 agconnect-services.json。


### 打开推送服务开关

1. 在华为推送平台，单击【全部服务】>【推送服务】，进入推送服务页面。
2. 在“推送服务”页面，单击【立即开通】，详情请参见 [打开推送服务开关](https://developer.huawei.com/consumer/cn/doc/distribution/app/agc-enable_service#enable-service)。

## SDK 集成（二选一）

### Android Studio Gradle 自动集成

1. 在安卓项目级目录 build.gradle 文件，【buildscript】>【 repositories & dependencies】下分别添加华为仓库地址和 HMS gradle 插件依赖：
```
buildscript {
    repositories {
        google()
        jcenter()
        maven {url 'http://developer.huawei.com/repo/'}     // 华为 maven 仓库地址
    }
    dependencies {
        // 其他classpath配置
        classpath 'com.huawei.agconnect:agcp:1.3.1.300'     // 华为推送 gradle 插件依赖
    }
}
```
2. 在安卓项目级目录 build.gradle 文件，【allprojects】>【repositories】下添加华为依赖仓库地址：
```
allprojects {
    repositories {
        google()
        jcenter()
        maven {url 'http://developer.huawei.com/repo/'}     // 华为 maven 仓库地址
    }
}
```
3. 将从华为推送平台获取的应用配置文件 agconnect-services.json 拷贝到 app 模块目录下。  
 ![](https://main.qcloudimg.com/raw/338c87faaeb388f648835f17aeddc490.png)
4. 在 app 模块下 build.gradle 文件头部添加以下配置：
```
// app 其他 gradle 插件
apply plugin: 'com.huawei.agconnect'      // HMS SDK gradle 插件
android {
    // app 配置内容
}
```
5. 在 app 模块下 build.gradle 文件内导入华为推送相关依赖：
```
dependencies {
		// ... 程序其他依赖
		implementation 'com.tencent.tpns:huawei:[VERSION]-release'      //  华为推送 [VERSION] 为当前最新 SDK 版本号，版本号可在 Android SDK 发布动态 查看
		implementation 'com.huawei.hms:push:5.0.2.300'       // HMS Core Push 模块依赖包
		}
```

>?
>- 华为推送 \[VERSION\] 为当前最新 SDK 版本号，版本号可在 [Android SDK 发布动态](https://intl.cloud.tencent.com/document/product/1024/36191) 查看。
>- TPNS Android SDK 自 1.2.1.3 版本起正式支持华为推送 V5 版本，请使用 1.2.1.3 及以上版本的 TPNS 华为依赖以避免集成冲突问题。


### Android Studio 手动集成

针对开发者内部构建环境无法访问华为 maven 仓库的情况，提供以下手动集成方法。

1. 下载 [SDK 安装包](https://console.cloud.tencent.com/tpns/sdkdownload)。
2. 打开 Other-Push-jar 文件夹， 导入 huaweiv5 推送相关依赖包，将全部 jar、aar 包复制到项目工程中。
3. 在安卓项目级目录 build.gradle 文件，【buildscript】>【dependencies】下添加 HMS gradle 插件的依赖：
```
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        // 其他 classpath 配置
        classpath files('app/libs/agcp-1.3.1.300.jar')     // 华为推送 gradle 插件依赖
    }
}
```
4. 将从华为推送平台获取的应用配置文件 agconnect-services.json 拷贝到 app 模块目录下。  
![](https://main.qcloudimg.com/raw/447e6453a5a996128b12c5ca9cdb10c7.png)
5. 在 app 模块下 build.gradle 文件头部添加以下配置：
```
// app 其他 gradle 插件
apply plugin: 'com.huawei.agconnect'      // HMS SDK V4 gradle 插件
android {
    // app 配置内容
}
```
6. 在 app 模块下 build.gradle 文件内导入华为推送相关依赖：
```
dependencies {
        // ... 程序其他依赖
        implementation files('libs/tpns-huaweiv5-1.2.1.1.jar')      // 适用于 HMS Core 版本的 TPNS 插件
        implementation fileTree(include: ['*.aar'], dir: 'libs')    // HMS Core Push 模块依赖包
    }
```
7. 在 manifest 文件 `<application> </application>` 标签内添加以下组件：
```
<application>
        <service
            android:name="com.huawei.android.hms.tpns.HWHmsMessageService"
            android:exported="false">
            <intent-filter>
                <action android:name="com.huawei.push.action.MESSAGING_EVENT" />
            </intent-filter>
        </service>
</application>
```

## 启动华为推送

在调用 TPNS 注册接口 `XGPushManager.registerPush` 前，开启第三方推送接口：

```
//打开第三方推送
XGPushConfig.enableOtherPush(getApplicationContext(), true);
```

注册成功的日志如下：

```
V/TPush: [XGPushConfig] isUsedOtherPush:true
E/xg.vip: get otherpush errcode: errCode : 0 , errMsg : success
V/TPush: [XGPushConfig] isUsedOtherPush:true
I/TPush: [OtherPushClient] handleUpdateToken other push token is : IQAAAACy0PsqAADxfCrWG3kupbOraeAiYoo9n2B-bAfb2d--kctc8E_UnY_mrIdg9ionukZvC******dVD8GlJi_5-0rpskunnNMcat35HA other push type: huawei
```

## 代码混淆

```plaintext
-ignorewarnings
-keepattributes *Annotation* 
-keepattributes Exceptions 
-keepattributes InnerClasses 
-keepattributes Signature 
-keepattributes SourceFile,LineNumberTable 
-keep class com.hianalytics.android.**{*;} 
-keep class com.huawei.updatesdk.**{*;} 
-keep class com.huawei.hms.**{*;}
-keep class com.huawei.agconnect.**{*;}
```


> ?混淆规则需要放在 App 项目级别的 proguard-rules.pro 文件中。

## 高级配置（可选）

### 华为通道抵达回执配置

华为通道抵达回执需要开发者自行配置，您可参见 [华为厂商通道回执配置指引](https://intl.cloud.tencent.com/document/product/1024/35246) 进行配置。完成后，可在推送记录中查看华为推送通道的抵达数据。
![](https://main.qcloudimg.com/raw/11c44dfc000045458a627e12b67ef611.png)

### 华为设备角标适配

华为设备支持设置应用角标，需要开发者申请应用内角标设置和设置应用启动类权限，详情请参见 [角标适配指南](https://intl.cloud.tencent.com/document/product/1024/35828) 文档。

## 常见问题排查

#### 华为推送注册错误码查询方法

华为推送服务接入过程配置要求较严格，若华为厂商通道注册失败，开发者可以通过以下方式获取华为推送注册错误码：


1. 推送服务 debug 模式下，过滤关键字“OtherPush”或“HMSSDK” ，查看相关返回码日志。
2. 错误码可在 [华为开发文档](https://developer.huawei.com/consumer/cn/doc/development/HMS-2-References/hmssdk_huaweipush_api_reference_errorcode) 查找对应原因，获取解决办法。



#### 通过华为通道下发的通知，为什么没有通知提醒？


华为推送从 EMUI 10.0版本开始将通知消息智能分成两个级别：一般与重要。EMUI 10.0之前的版本没有对通知消息进行分类，只有一个级别，消息全部通过“默认通知”渠道展示，等价于 EMUI 10.0的重要级别消息。若通知被归类为“一般”级别，则没有震动、响铃、和状态栏图标提示，目前可通过自定义通知渠道将消息级别设为“重要”；但遵照华为推送相关规则，最终展示效果仍将与华为推送智能分类计算出的级别共同决定，两者取低，例如：重要与一般取一般。详情请参见 [华为通知渠道使用指南](https://intl.cloud.tencent.com/document/product/1024/36250)。


#### 其他

如遇到发布华为应用市场，发布应用时审核不通过，显示“错误:28: 集成 HMS 需要将证书文件打包到 APK 中，请直接将 assets 目录拷贝到应用工程根目录”。请按如下方法解决：
1. 下载华为官方 HMS SDK。
2. 将 assets 目录下的所有文件及子目录拷贝到开发者 App 工程的同名目录下。如果目录不存在，请先创建。

