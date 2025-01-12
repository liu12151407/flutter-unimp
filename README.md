# flutter_unimp

使用了uni小程序功能，小程序源码版本，目前没发到pub.dev。

[unimp官网](https://nativesupport.dcloud.net.cn/)

iOS SDK：4.15

Android SDK：4.15

```yaml
flutter_unimp:
    git:
      url: https://github.com/lljwdbklb/flutter-unimp.git
```

## api

```dart

String appid = "__UNI__11E9B73";
String filePath = "wgt资源位置";

final _flutterUnimpPlugin = FlutterUnimp();

/// 运行目录中是否已经存在小程序资源
bool isExists = await _flutterUnimpPlugin.isExistsUniMP(appId: appid);

/// 将wgt资源部署到运行路径中
bool isInstall = await _flutterUnimpPlugin.installUniMPResource(appId: appid, wgtPath: filePath);

/// 获取已经部署的小程序应用资源版本信息
/// 返回数据为 manifest 中的配置信息
/// {
///     "name": "1.0.0",     // 应用版本名称
///     "code": 100          // 应用版本号
/// }
Map? versionInfo = await _flutterUnimpPlugin.getUniMPVersionInfo(appId: appid);

/// 启动小程序
Map? _flutterUnimpPlugin.openUniMP(appId: appid, arguments: { "launchInfo": "Hello UniMP" });

/// 关闭当前显示的小程序应用
_flutterUnimpPlugin.closeUniMP();

/// 向当前打开的小程序发送事件
_flutterUnimpPlugin.sendUniMPEvent(event: 'event', data: {"launchInfo": "Hello UniMP"});

/// 小程序向原生发送消息的监听器
_flutterUnimpPlugin.registerListener((call) aync {
    return Future(() => {"data":"回调给小程序"})
})

```

## 功能模块支持

| 模块名                           | 5+APP项目                   | Uni API                           | 是否支持 |
| -------------------------------- | :-------------------------- | :-------------------------------- | -------- |
| Camera(摄像头)/Gallery(图片选择) | plus.camera                 | image                             | 是       |
| Accelerometer(加速度传感器)      | plus.accelerometer          | Accelerometer                     | 是       |
| Audio(音频)                      | plus.audio                  | record-manager<br />audio-context | 是       |
| Contacts(通讯录)                 | plus.contacts               | contact                           | 是       |
| File(文件系统)                   | plus.io                     | file                              | 是       |
| Geolocation(高德定位)            | plus.geolocation            | location                          | 是       |
| native.js                        | plus.ios                    |                                   | 是       |
| Messaging(短彩邮件消息)          | plus.messaging              |                                   | 是       |
| Orientation(设备方向)            | plus.orientation            |                                   | 是       |
| Proximity(距离传感器)            | plus.proximity              |                                   | 是       |
| XMLHttpRequest(网络请求)         | plus.net                    | request                           | 是       |
| zip(解压缩)                      | plus.zip                    |                                   | 是       |
| Barcode(扫码)                    | plus.barcode                | barcode                           | 是       |
| Maps（高德地图）                 | plus.maps                   | map                               | 是       |
| Payment（支付）                  | plus.payment                | payment                           | 否       |
| Share(分享)                      | plus.share                  | share                             | 否       |
| Speech(语音识别)                 | plus.speech                 | voice                             | 否       |
| Statistic(友盟统计)              | plus.statistic              |                                   | 是       |
| Oauth（授权登陆）                | plus.oauth                  | login                             | 否       |
| Video（视频播放）                | plus.video                  | video                             | 是       |
| fingerprint(指纹识别)            | plus.fingerprint            | authentication                    | 是       |
| faceId（人脸识别）               |                             | authentication                    | 是       |
| BlueTooth(蓝牙)                  | plus.bluetooth              | bluetooth                         | 是       |
| sqlite（数据库）                 | plus.sqlite                 |                                   | 是       |
| livepusher(直播推流)             | plus.video.createLivePusher | createliveplayercontext           | 是       |
| iBeacon                          | plus.ibeacon                | ibeacon                           | 是       |

### iOS权限设置

在info.plist中添加以下权限，描述根据自己情况自行修改:

```plist
<key>NSCameraUsageDescription</key>
<string>使用相机</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>使用相册</string>
<key>NSPhotoLibraryAddUsageDescription</key>
<string>添加图片到相册</string>
<key>NSMicrophoneUsageDescription</key>
<string>使用麦克风</string>
<key>NSContactsUsageDescription</key>
<string>使用通讯录</string>
<key>NSLocationUsageDescription</key>
<string>使用定位</string>
<key>NSLocationWhenInUseUsageDescription</key>
<string>使用定位</string>
<key>NSLocationAlwaysUsageDescription</key>
<string>使用定位</string>
<key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
<string>使用定位</string>
<key>NSFaceIDUsageDescription</key>
<string>使用脸部识别</string>
<key>NSBluetoothPeripheralUsageDescription</key>
<string>使用蓝牙</string>
<key>NSBluetoothAlwaysUsageDescription</key>
<string>使用蓝牙</string>
<key>amap</key>
<dict>
	<key>appkey</key>
	<string>去官方网站申请对应的值</string>
</dict>
```

### Android权限设置

```
    <!-- Barcode(二维码)  begin -->
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

    <uses-feature android:name="android.hardware.camera" />
    <uses-feature android:name="android.hardware.camera.autofocus" />

    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.FLASHLIGHT" />
    <!-- Barcode(二维码)  end -->

    <uses-permission android:name="android.permission.USE_FINGERPRINT" />

    <!-- Maps(地图) begin -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.WRITE_SETTINGS" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
    <uses-permission android:name="android.permission.READ_LOGS" />
    <!-- Maps(地图) end -->


    <!-- Share(分享)  begin -->
    <!-- Share - 新浪微博分享 -->
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <!-- Share - 微信分享 -->
    <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />


    <!-- Speech(语音识别)  begin -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <!-- Speech(语音识别)  end -->


    <!-- Statistic(统计)  begin -->
    <!-- Statistic - 友盟统计 -->
    <uses-permission android:name="android.permission.READ_LOGS" />
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
    <uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
    <!-- Statistic(统计)  end -->

    <!-- 蓝牙 ibeacon权限-->
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
    <uses-permission android:name="android.permission.BLUETOOTH" />

    <!-- 基座删除的部分权限 -->
    <uses-permission android:name="android.permission.GET_TASKS" />
    <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE" />
    <uses-permission android:name="android.permission.READ_CONTACTS" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />

    <uses-feature android:name="android.hardware.camera.autofocus" />

    <uses-permission android:name="android.permission.WRITE_CONTACTS" />
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.GET_ACCOUNTS" />
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <uses-permission android:name="android.permission.SEND_SMS" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.FLASHLIGHT" />

    <uses-feature android:name="android.hardware.camera" />

    <uses-permission android:name="android.permission.WRITE_SMS" />
    <uses-permission android:name="android.permission.READ_SMS" />

    <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE_CONNECTED_DEVICE" />
```

## 代码贡献
[Hyde Huang](https://github.com/szhyde)
[WhoJun](https://github.com/lljwdbklb)
