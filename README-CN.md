- [1 接入 Atmosplay Ads SDK 和 AdMob SDK](#1-%e6%8e%a5%e5%85%a5-atmosplay-ads-sdk-%e5%92%8c-admob-sdk)
  - [1.1 添加 Atmosplay Ads SDK 依赖](#11-%e6%b7%bb%e5%8a%a0-atmosplay-ads-sdk-%e4%be%9d%e8%b5%96)
  - [1.2 添加 AdMob 广告 SDK 依赖](#12-%e6%b7%bb%e5%8a%a0-admob-%e5%b9%bf%e5%91%8a-sdk-%e4%be%9d%e8%b5%96)
  - [1.3 将 Atmosplay Adapter 导入到工程中](#13-%e5%b0%86-atmosplay-adapter-%e5%af%bc%e5%85%a5%e5%88%b0%e5%b7%a5%e7%a8%8b%e4%b8%ad)
- [2 在AdMob 平台添加 Atmosplay Ads 广告源](#2-%e5%9c%a8admob-%e5%b9%b3%e5%8f%b0%e6%b7%bb%e5%8a%a0-atmosplay-ads-%e5%b9%bf%e5%91%8a%e6%ba%90)
  - [2.1 添加新应用](#21-%e6%b7%bb%e5%8a%a0%e6%96%b0%e5%ba%94%e7%94%a8)
  - [2.2 添加新广告位](#22-%e6%b7%bb%e5%8a%a0%e6%96%b0%e5%b9%bf%e5%91%8a%e4%bd%8d)
  - [2.3 添加 Atmosplay Ads 广告源](#23-%e6%b7%bb%e5%8a%a0-atmosplay-ads-%e5%b9%bf%e5%91%8a%e6%ba%90)
- [3 测试](#3-%e6%b5%8b%e8%af%95)

## 1 接入 Atmosplay Ads SDK 和 AdMob SDK

以 Android Studio 为例，接入 AdMob 请查看[AdMob SDK 接入文档](https://developers.google.com/admob/android/quick-start)，以下简要步骤

### 1.1 添加 Atmosplay Ads SDK 依赖

在 app Module 的 build.gradle 文件中添加

```
dependencies {
    implementation 'com.atmosplayads:atmosplayads:3.0.0'
}
```

### 1.2 添加 AdMob 广告 SDK 依赖

a. 在 project 构建文件(gradle)中的 allprojects.repositories 结点添加以下代码

```
maven {
    url "https://maven.google.com"
}
```

使其看起来像：

```
allprojects {
    repositories {
        maven {
            url "https://maven.google.com"
        }
    }
}
```

b. 在 app Module 的 build.gradle 文件中添加（可选）

```
dependencies {
    implementation 'com.google.android.gms:play-services-ads:17.2.0'
}
```

### 1.3 将 Atmosplay Adapter 导入到工程中

- Bannder Adapter：[AtmosplayAdsBanner.java](./admobadapter/src/main/java/com/atmosplayads/admobadapter/AtmosplayAdsBanner.java)

- 插屏 Adapter：[AtmosplayAdsInterstitial.java](./admobadapter/src/main/java/com/atmosplayads/admobadapter/AtmosplayAdsInterstitial.java)

- 激励视频 Adapter：[AtmosplayRewardedVideo.java](./admobadapter/src/main/java/com/atmosplayads/admobadapter/AtmosplayRewardedVideo.java)

- Admob 激励视频老版本的 Adapter：[AtmosplayAdsRewardedVideoLegacy.java](./admobadapter/src/main/java/com/atmosplayads/admobadapter/AtmosplayAdsRewardedVideoLegacy.java)

*若是Unity开发环境，请将上述文件添加到项目的`Assets/Plugins/Android`目录下。*

工具类(包含解析 admob 后台配置的信息，转换错误码等功能)：[AtmosplayAdsUtil.java](./admobadapter/src/main/java/com/atmosplayads/admobadapter/AtmosplayAdsUtil.java)

> 关于适配类和请求的详细内容，请参考[DEMO](https://github.com/Atmosplay/AdMobAdapter-AtmosplayAds-Android)中的代码。

## 2 在[AdMob 平台](https://apps.admob.com/v2/home)添加 Atmosplay Ads 广告源

### 2.1 添加新应用

a. 选择目录中 Apps，点击“ADD APP”按钮
![image](imgs/018addapp1.png)

b. 选择您的应用是否已经上架 Google Play 或 App Store，如果已上架，选择“YES”，如果未上架，选择“NO”，以下以未上架为例
![image](imgs/018addapp2.png)

c. 输入应用名称，选择应用操作系统，点击“ADD”保存添加的应用
![image](imgs/019addapp3.png)

### 2.2 添加新广告位

a. 添加应用后，点击“NEXT: CREATE AD UNIT”按钮可为此应用添加广告位
![image](imgs/addunit.png)

b. 选择您所需要的广告形式，Atmosplayads Ads 目前支持 Banner, Interstitial 及 Rewarded，此处以 Rewarded 为例
![image](imgs/003addadunit2RV1.png)

c. 输入广告位名称并点击“CREATE AD UNIT”保存添加的广告位

![image](imgs/004addadunit2RV2.png)

d. 获取此广告位的 app ID 及 ad unit ID，点击“DONE”完成广告位的创建

![image](imgs/005addadunit2RV3.png)

### 2.3 添加 Atmosplay Ads 广告源

a. 目录中选择“[Mediation](https://apps.admob.com/v2/mediation/groups/list)”，选择“CREATE MEDIATION GROUP”

![image](imgs/007mediationgroupcreate.png)

b. 选择您要使用的广告形式及操作系统，Atmosplayads Ads 目前支持 Banner, Interstitial 及 Rewarded，此处以 Rewarded 为例，点击“CONTINUE”进入下一步

![image](imgs/008mediationgroupcreate1.png)

c. 输入 Mediation 名字，通过 Location 进行地域设置，状态置位 Enable 时 Mediation 才可生效，请确保状态为 Enable。点击“ADD AD UNIT”选择要添加的广告位

![image](imgs/009mediationgroupcreat2.png)

d. 在广告位选择框中，先后选择所需应用及广告位，点击“DONE”保存所配置的广告位

![image](imgs/011mediationgroupcreate4.png)

e. 点击“ADD CUSTOM EVENT”添加自定义广告源

![image](imgs/012mediationgroupcreate5.png)

f. 输入第三方广告源名称，此处以 Atmosplay Network 为例，可根据需求进行自定义，根据需要对第三方广告源进行价格设置

![image](imgs/013mediationgroupcreate6.png)

g. 对 Atmosplay Network 广告源进行配置。在 Class Name 中填写完整的适配器类名，以 demo 中适配器类名为例，

Banner 为

`com.atmosplayads.admobadapter.AtmosplayAdsBanner`

插屏为

`com.atmosplayads.admobadapter.AtmosplayAdsInterstitial`

激励视频为

`com.atmosplayads.admobadapter.AtmosplayAdsRewardedVideo`

Parameter 中需填写您在 Atmosplay Ads 申请的[应用 ID](https://sellers.atmosplay.net/#/app/appList/)和[广告位 ID](https://sellers.atmosplay.net/#/ad/placeList/)两个参数，点击“DONE”完成 Atmosplay Ads 的配置

```json
{ "appId": "youAppId", "unitId": "yourUnitId" }
```

![image](imgs/014mediationgroupcreate7.png)

h. Ad source 列表中可以看到所设置的广告源 Atmosplay Network，点击“SAVE”完成 Mediation 的配置

![image](imgs/015mediationgroupcreate8.png)

i. 检查第三方广告源是否添加完成，在[Apps 列表](https://apps.admob.com/v2/apps/list)中找到步骤 d 中选择的应用及广告位，广告位 Mediation groups 中 active 数量增加表示广告源添加成功

![image](imgs/016mediationgroupcreate9.png)

## 3 测试

您在测试中可使用如下 ID 进行测试，测试 ID 不会产生收益，应用上线时请使用您在[Atmosplay Ads](https://sellers.atmosplay.net/#/app/appList/)申请的正式 ID。

| 广告形式    | App_ID                               | Ad_Unit_id                           |
| ----------- | ------------------------------------ | ------------------------------------ |
| Banner 广告 | 5C5419C7-A2DE-88BC-A311-C3E7A646F6AF | F22F347B-3D57-0C70-0B13-EFCFDF402EBA |
| 激励视频    | 5C5419C7-A2DE-88BC-A311-C3E7A646F6AF | 3FBEFA05-3A8B-2122-24C7-A87D0BC9FEEC |
| 插屏广告    | 5C5419C7-A2DE-88BC-A311-C3E7A646F6AF | 19393189-C4EB-3886-60B9-13B39407064E |
