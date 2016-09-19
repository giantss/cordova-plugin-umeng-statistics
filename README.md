# Umeng PhoneGap SDK 集成文档

## 概述
  Umeng PhoneGap SDK 适用于Cordova和PhoneGap跨平台项目。
  统计所有指标，均和标准移动统计完全相同。

## 集成文档

### 下载

   在官方地址下载最新版本的[友盟+统计分析SDK](http://dev.umeng.com/analytics/android-doc/sdk-download)


### 导入SDK
    - 将下载的最新的umeng*.jar替换umeng-plugin-android/src/android/中的最新jar  

### 基本功能集成

* 配置manifest和appkey
    
    - 修改umeng-plugin-android/plugin.xml文件：
        * umeng-analytics-v6.0.0.jar修改为最新的jar名字；
        * UMENG_APPKEY 的value修改为友盟官方申请的appkey
        ![umappkey](http://dev.umeng.com/system/images/W1siZiIsIjIwMTQvMDEvMTcvMTNfNTJfMzBfMjI4X2RldjUucG5nIl1d/dev5.png "Umeng-Appkey") 
        * UMENG_CHANNEL 的value修改为渠道
    
    - 如果不在manifest里配置友盟的appkey,可以在html代码的body 的onload()时候调用此接口：`MobclickAgent.init("appkey", "channel");`

* 新建工程步骤

    - 创建工程 `cordova create hello`
    
    - 创建android工程 `cordova platforms add android`
    
    - 依赖友盟的SDK `cordova plugins add */umeng-plugin-android/`


* 在主界面集成友盟初始化

        /**
         * onCreate中调用
         */
        private void initUmengSDK() {
            MobclickAgent.setScenarioType(this, EScenarioType.E_UM_NORMAL);
            MobclickAgent.setDebugMode(true);
            MobclickAgent.openActivityDurationTrack(false);
            // MobclickAgent.setSessionContinueMillis(1000);
        }
    
        @Override
        protected void onResume() {
            super.onResume();
            MobclickAgent.onResume(this);
        }
    
        @Override
        protected void onPause() {
            super.onPause();
            MobclickAgent.onPause(this);
        }


* 统计方法使用
    
- JavaScript方法介绍

    *  MobclickAgent.getDeviceId(deviceId) 获取Android IMEI
    *  MobclickAgent.onEvent(eventId)  自定义事件
    *  MobclickAgent.onCCEvent(evenArray, evenValue, eventLabel) 结构化自定义事件
    *  MobclickAgent.onEventWithLabel(eventId, eventLabel) 自定义事件
    *  MobclickAgent.onEventWithParameters(eventId, eventData) 自定义事件
    *  MobclickAgent.onEventWithCounter(eventId, eventData, eventNum) 自定义事件
    *  MobclickAgent.onPageBegin(pageName) 页面开始的时候调用此方法
    *  MobclickAgent.onPageEnd(pageName) 页面结束的时候调用此方法
    *  MobclickAgent.profileSignInWithPUID(puid) 统计帐号登录接口
    *  MobclickAgent.profileSignInWithPUIDWithProvider(puid, provider)  统计帐号登录接口
    *  MobclickAgent.profileSignOff()      帐号统计退出接口
    *  MobclickAgent.setUserLevelId(level) 当玩家建立角色或者升级时,需调用此接口
    *  MobclickAgent.startLevel(level) 在游戏开启新的关卡的时候调用
    *  MobclickAgent.finishLevel(level) 关卡结束时候调用
    *  MobclickAgent.failLevel(level) 关卡失败时候调用
    *  MobclickAgent.exchange(orderId, currencyAmount, currencyType, virtualAmount, channel) 真实消费统计
    *  MobclickAgent.pay(cash, source, coin) 真实消费统计
    *  MobclickAgent.payWithItem(cash, source, item, amount, price) 真实消费统计
    *  MobclickAgent.buy(item, amount, price)  虚拟消费统计
    *  MobclickAgent.use(item, amount, price)  物品消耗统计
    *  MobclickAgent.bonusWithItem(item, amount, price, source) 额外奖励
    *  MobclickAgent.(coin, source) 额外奖励
    *  MobclickAgent.setLogEnabled(enabled) log是否进入调试模式


    - Android标准统计方法可以正常使用.具体参考 [友盟+统计分析](http://dev.umeng.com/analytics/android-doc/integration) 和 [友盟+游戏统计分析](http://dev.umeng.com/game_analytics/game-android/integration)

### 代码混淆

 集成完毕后，如果你的应用使用了混淆,请添加：

    -keepclassmembers class * {
       public <init> (org.json.JSONObject);
    }
    
    这是由于SDK中的部分代码使用反射来调用构造函数， 如果被混淆掉， 在运行时会提示"NoSuchMethod"错误。 另外，由于SDK需要引用导入工程的资源文件，通过了反射机制得到资源引用文件R.java，但是在开发者通过proguard等混淆/优化工具处理apk时，proguard可能会将R.java删除，如果遇到这个问题，请在proguard配置文件中添加keep命令如：
    
    -keep public class [您的应用包名].R$*{
    public static final int *;
    }
    
    把[您的应用包名] 替换成您自己的包名，如com.yourcompany.example。如果您使用5.0.0及以上版本的SDK，请添加如下命令：
    
    -keepclassmembers enum * {
        public static **[] values();
        public static ** valueOf(java.lang.String);
    }
    把[您的应用包名] 替换成您自己的包名
    -keep public class [您的应用包名].UMHybrid { *;}
	
	# Umeng PhoneGap SDK 集成文档

## 概述
  Umeng PhoneGap SDK 适用于Cordova和PhoneGap跨平台项目。
  统计所有指标，均和标准移动统计完全相同。

## 集成文档

### 下载

   在官方地址下载最新版本的[友盟+统计分析SDK](http://dev.umeng.com/analytics/ios-doc/sdk-download)


### 导入SDK
    - 访问 [Umeng 官网](http://www.umeng.com/) 下载最新版本的 iOS 平台 Analytics SDK。Plugin 中的 SDK 可能不是最新版本，需要检查并使用刚刚下载的新版本，进入克隆到本地的 Plugin 目录：
    使用最新版本 SDK 的 `UMMobClick.framework`  Plugin 中 `src\ios` 文件夹下的同名文件。

### 基本功能集成


* 新建工程步骤

    - 创建工程 `cordova create hello`
    
    - 创建ios工程 `cordova platforms add ios`
    
    - 依赖友盟的SDK `cordova plugins add [Plugin 路径]`


* 在主界面集成友盟初始化

在 `%Cordova工程目录%\/platforms/ios/demo/Classes/AppDelegate.m` 文件中，找到方法 `(BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions`，添加下面的代码：

UMConfigInstance.appKey = @"Your Appkey";
UMConfigInstance.channelId = @"Your ChannelId";"

UMConfigInstance.eSType=E_UM_GAME;//友盟游戏统计，如不设置默认为应用统计

[MobClick startWithConfigure:UMConfigInstance];


同样的，`[Your Appkey]` 就是刚刚申请的 Appkey，`[Your ChannelId]` 是应用的渠道号。
    

* 统计方法使用
    
- JavaScript方法介绍

    *  MobclickAgent.getDeviceId(deviceId) 获取Android IMEI
    *  MobclickAgent.onEvent(eventId)  自定义事件
    *  MobclickAgent.onCCEvent(evenArray, evenValue, eventLabel) 结构化自定义事件
    *  MobclickAgent.onEventWithLabel(eventId, eventLabel) 自定义事件
    *  MobclickAgent.onEventWithParameters(eventId, eventData) 自定义事件
    *  MobclickAgent.onEventWithCounter(eventId, eventData, eventNum) 自定义事件
    *  MobclickAgent.onPageBegin(pageName) 页面开始的时候调用此方法
    *  MobclickAgent.onPageEnd(pageName) 页面结束的时候调用此方法
    *  MobclickAgent.profileSignInWithPUID(puid) 统计帐号登录接口
    *  MobclickAgent.profileSignInWithPUIDWithProvider(puid, provider)  统计帐号登录接口
    *  MobclickAgent.profileSignOff()      帐号统计退出接口
    *  MobclickAgent.setUserLevelId(level) 当玩家建立角色或者升级时,需调用此接口
    *  MobclickAgent.startLevel(level) 在游戏开启新的关卡的时候调用
    *  MobclickAgent.finishLevel(level) 关卡结束时候调用
    *  MobclickAgent.failLevel(level) 关卡失败时候调用
    *  MobclickAgent.exchange(orderId, currencyAmount, currencyType, virtualAmount, channel) 真实消费统计
    *  MobclickAgent.pay(cash, source, coin) 真实消费统计
    *  MobclickAgent.payWithItem(cash, source, item, amount, price) 真实消费统计
    *  MobclickAgent.buy(item, amount, price)  虚拟消费统计
    *  MobclickAgent.use(item, amount, price)  物品消耗统计
    *  MobclickAgent.bonusWithItem(item, amount, price, source) 额外奖励
    *  MobclickAgent.(coin, source) 额外奖励
    *  MobclickAgent.setLogEnabled(enabled) log是否进入调试模式


    - ios标准统计方法可以正常使用.具体参考 [友盟+统计分析](http://dev.umeng.com/analytics/ios-doc/integration) 和 [友盟+游戏统计分析](http://dev.umeng.com/game_analytics/game-ios/integration)



