# wechat_kit

[![Build Status](https://cloud.drone.io/api/badges/v7lin/fake_wechat/status.svg)](https://cloud.drone.io/v7lin/fake_wechat)
[![Codecov](https://codecov.io/gh/v7lin/fake_wechat/branch/master/graph/badge.svg)](https://codecov.io/gh/v7lin/fake_wechat)
[![GitHub Tag](https://img.shields.io/github/tag/v7lin/fake_wechat.svg)](https://github.com/v7lin/fake_wechat/releases)
[![Pub Package](https://img.shields.io/pub/v/wechat_kit.svg)](https://pub.dartlang.org/packages/wechat_kit)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/v7lin/fake_wechat/blob/master/LICENSE)

flutter版微信SDK

## flutter toolkit

* [flutter版微信SDK](https://github.com/v7lin/fake_wechat)
* [flutter版腾讯(QQ)SDK](https://github.com/v7lin/fake_tencent)
* [flutter版新浪微博SDK](https://github.com/v7lin/fake_weibo)
* [flutter版支付宝SDK](https://github.com/v7lin/fake_alipay)
* [flutter版腾讯(信鸽)推送SDK](https://github.com/v7lin/fake_push)
* [flutter版talkingdata移动统计SDK](https://github.com/v7lin/fake_analytics)

## dart/flutter 私服

* [simple_pub_server](https://github.com/v7lin/simple_pub_server)

## docs

* [微信开放平台](https://open.weixin.qq.com/)
* [微信登录](https://open.weixin.qq.com/cgi-bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=open1419317851&token=&lang=zh_CN)
* [扫码登录](https://open.weixin.qq.com/cgi-bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=215238808828h4XN&token=&lang=zh_CN)
* [微信支付](https://open.weixin.qq.com/cgi-bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=open1419317780&token=&lang=zh_CN)
* [Universal Links](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content)

## android

```
# 不需要做任何额外接入工作
# 混淆已打入 Library，随 Library 引用，自动添加到 apk 打包混淆
```

```xml
<manifest>
    <!-- targetSdkVersion >= 29 && compileSdkVersion >= 29, 豁免 Android Q 的外部存储沙箱限制 -->
    <application android:requestLegacyExternalStorage="true">
    </application>
</manifest>
```

#### 获取 android 微信签名信息

非官方方法 -> 反编译 Gen_Signature_Android2.apk 所得

命令：

```shell
keytool -list -v -keystore ${your_keystore_path} -storepass ${your_keystore_password} 2>/dev/null | grep -p 'MD5:.*' -o | sed 's/MD5://' | sed 's/ //g' | sed 's/://g' | awk '{print tolower($0)}'
```

示例：

```shell
keytool -list -v -keystore example/android/app/infos/debug.keystore -storepass android 2>/dev/null | grep -p 'MD5:.*' -o | sed 's/MD5://' | sed 's/ //g' | sed 's/://g' | awk '{print tolower($0)}'
```

```shell
ce187ed67e05c2d8879bf66bbfdfc8b9
```

## ios

```
在Xcode中，选择你的工程设置项，选中“TARGETS”一栏，在“info”标签栏的“URL type“添加“URL scheme”为你所注册的应用程序id

URL Types
weixin: identifier=weixin schemes=${appId}
```

```
iOS 9系统策略更新，限制了http协议的访问，此外应用需要在“Info.plist”中将要使用的URL Schemes列为白名单，才可正常检查其他应用是否安装。

<key>LSApplicationQueriesSchemes</key>
<array>
    <string>weixin</string>
    <string>weixinULAPI</string>
</array>
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```

```
Universal Links

Capabilities -> Associated Domain -> Domain -> applinks:${your applinks}
```

## flutter

* snapshot

```
dependencies:
  wechat_kit:
    git:
      url: https://github.com/v7lin/fake_wechat.git
```

* release

```
dependencies:
  wechat_kit: ^${latestTag}
```

* example

[示例](./example/lib/main.dart)

## Getting Started

This project is a starting point for a Flutter
[plug-in package](https://flutter.dev/developing-packages/),
a specialized package that includes platform-specific implementation code for
Android and/or iOS.

For help getting started with Flutter, view our 
[online documentation](https://flutter.dev/docs), which offers tutorials, 
samples, guidance on mobile development, and a full API reference.
