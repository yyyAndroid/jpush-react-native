# JPush-React-Native

## ChangeLog

1. 从RN-JPush2.7.5开始，重新支持TypeScript
2. 由于RN-JCore1.6.0存在编译问题，从RN-JCore1.7.0开始，还是需要在AndroidManifest.xml中添加配置代码，具体参考 配置-2.1 Android


## 1. 安装

```
npm install jpush-react-native --save
```

* 注意：如果项目里没有jcore-react-native，需要安装

  ```
  npm install jcore-react-native --save
  ```
安装完成后连接原生库
进入到根目录执行<br/>
react-native link<br/>
或<br/>
react-native link jpush-react-native<br/>
react-native link jcore-react-native

## 2. 配置

### 2.1 Android

* build.gradle

  ```
  android {
        defaultConfig {
            applicationId "yourApplicationId"           //在此替换你的应用包名
            ...
            manifestPlaceholders = [
                    JPUSH_APPKEY: "yourAppKey",         //在此替换你的APPKey
                    JPUSH_CHANNEL: "yourChannel"        //在此替换你的channel

                    //xiaomi_config_start
                    XIAOMI_APPID  : "MI-小米的APPID",
                    XIAOMI_APPKEY : "MI-小米的APPKEY",
                    //xiaomi_config_end
                    //oppo_config_start
                    OPPO_APPKEY   : "OP-oppo的APPKEY",
                    OPPO_APPID    : "OP-oppo的APPID",
                    OPPO_APPSECRET: "OP-oppo的APPSECRET",
                    //oppo_config_end
                    //vivo_config_start
                    VIVO_APPKEY   : "vivo的APPKEY",
                    VIVO_APPID    : "vivo的APPID",
                    //vivo_config_end
            ]
        }
    }
  ```

  ```
  dependencies {
        ...
        implementation project(':jpush-react-native')  // 添加 jpush 依赖
        implementation project(':jcore-react-native')  // 添加 jcore 依赖
    }
  ```

  ```
  //huawei_plugin_start
  //华为请按照厂商文档配置根 gradle 华为镜像依赖和添加 agconnect-services.json 后再打开此插件依赖
  //在华为应用服务控制台下载配置文件 agconnect-services.json 并放置到应用主工程的 assets 目录下
  //apply plugin: 'com.huawei.agconnect'
  //huawei_plugin_end
  ```

* setting.gradle

  ```
  include ':jpush-react-native'
  project(':jpush-react-native').projectDir = new File(rootProject.projectDir, '../node_modules/jpush-react-native/android')
  include ':jcore-react-native'
  project(':jcore-react-native').projectDir = new File(rootProject.projectDir, '../node_modules/jcore-react-native/android')
  ```

### 2.2 iOS
注意：您需要打开ios目录下的.xcworkspace文件修改您的包名

### 2.2.1 pod

```
pod install
```

* 注意：如果项目里使用pod安装过，请先执行命令

  ```
  pod deintegrate
  ```

### 2.2.2 手动方式

* Libraries

  ```
  Add Files to "your project name"
  node_modules/jcore-react-native/ios/RCTJCoreModule.xcodeproj
  node_modules/jpush-react-native/ios/RCTJPushModule.xcodeproj
  ```

* Capabilities

  ```
  Push Notification --- ON
  ```

* Build Settings

  ```
  All --- Search Paths --- Header Search Paths --- +
  $(SRCROOT)/../node_modules/jcore-react-native/ios/RCTJCoreModule/
  $(SRCROOT)/../node_modules/jpush-react-native/ios/RCTJPushModule/
  ```

* Build Phases

  ```
  libz.tbd
  libresolv.tbd
  UserNotifications.framework
  libRCTJCoreModule.a
  libRCTJPushModule.a
  ```

## 3. 引用

### 3.1 Android

参考：[MainApplication.java](https://github.com/jpush/jpush-react-native/tree/master/example/android/app/src/main/java/com/example/MainApplication.java)

### 3.2 iOS

参考：[AppDelegate.m](https://github.com/jpush/jpush-react-native/tree/master/example/ios/example/AppDelegate.m) 

### 3.3 js

参考：[App.js](https://github.com/jpush/jpush-react-native/blob/dev/example/App.js) 

## 4. API

详见：[index.js](https://github.com/jpush/jpush-react-native/blob/master/index.js)

## 5.  其他

* 集成前务必将example工程跑通
* 如有紧急需求请前往[极光社区](https://community.jiguang.cn/c/question)
* 上报问题还麻烦先调用JPush.setLoggerEnable(true}，拿到debug日志

 

