# cordova-plugin-umeng-statistics

友盟统计插件

## 功能

- 自定义事件
- 结构化自定义事件
- 页面开始的时候调用此方法
- 页面结束的时候调用此方法
- 统计帐号登录接口
- 统计帐号登录接口
- 帐号统计退出接口
- 当玩家建立角色或者升级时,需调用此接口
- 在游戏开启新的关卡的时候调用
- 关卡结束时候调用
- 关卡失败时候调用
- 真实消费统计
- 真实消费统计
- 真实消费统计
- 虚拟消费统计
- 物品消耗统计
- 额外奖励
- 额外奖励
- log是否进入调试模式


##安装要求
- Cordova Version >=5.0
- Cordova-Android >=4.0
- Cordova-iOS >=6.0




##安装
1. 命令行运行      ```cordova plugin add https://github.com/giantss/cordova-plugin-umeng-statistics.git```
2. 命令行运行 cordova build --device

##注意事项
1. 这个插件要求cordova-Android 的版本 >=4.0,推荐使用 cordova  5.0.0 或更高的版本，因为从cordova 5.0 开始cordova-Android 4.0 是默认使用的Android版本
2. 请在cordova的deviceready事件触发以后再调用本插件！！！




## 使用方式

- 插件初始化
```Javascript
/**参数说明
 *参数一: 注册友盟后台可以拿到
 *参数二 :这个参数是在后台统计app下载的渠道，会形成表格视图下载比例，androidChannelId可以下载app的android渠道 比如 应用宝可以简写成yjb 这是自定义的 iosChannelId不多说只有一个apple store
 **/
Umeng.init(UM_ANDROID_APPKEY/UM_IOS_APPKEY, androidChannelId/iosChannelId);

```



## License

<a href="http://www.opensource.org/licenses/mit-license.html">The MIT License (MIT)</a>