---
title: スタンドアロン Media SDKからAdobe Launchへの移行 – iOS
description: Media SDK から iOS 用の Launch に移行する方法を説明します。
exl-id: f70b8e1b-cb9f-4230-86b2-171bdaed4615
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/drdnQd83UXJkMKj-isUKPeIHe9xGetwY31HzHf37IEo
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 429
ht-degree: 60%

---

# スタンドアロンの Media SDK から Adobe Launch への移行 - iOS

>[!NOTE]
>Adobe Experience Platform Launch は、Experience Platform のデータ収集テクノロジースイートとしてリブランドされています。 その結果、製品ドキュメント全体でいくつかの用語の変更がロールアウトされました。 用語の変更点の一覧については、次の[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ja)を参照してください。

## 設定

### スタンドアロンの Media SDK

スタンドアロンのMedia SDKでは、アプリでトラッキング設定を設定し，
SDKに渡します。

```objective-c
ADBMediaHeartbeatConfig *config =
  [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"v2.0.0";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### Launch 拡張機能

1. Experience Platform Launch　で、モバイルプロパティの「[!UICONTROL 拡張機能]」タブをクリックします。
1. 「[!UICONTROL カタログ]」タブでオーディオおよびビデオ用 Adobe Media Analytics 拡張機能を探し、「[!UICONTROL インストール]」をクリックします。
1. 拡張機能の設定ページで、トラッキングパラメーターを設定します。
メディア拡張機能では、設定済みのパラメーターをトラッキングに使用します。

   ![](assets/launch_config_mobile.png)

[Media Analytics拡張機能の設定](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

## トラッカーの作成

### スタンドアロンの Media SDK

スタンドアロン Media SDKでは、`ADBMediaHeartbeatConfig` オブジェクトを手動で作成します
トラッキングパラメーターを設定します。 を公開するデリゲート インターフェイスを実装します。
`getQoSObject()` と `getCurrentPlaybackTime()functions.`

トラッキング用の MediaHeartbeat インスタンスの作成：

```objective-c
@interface PlayerDelegate : NSObject<ADBMediaHeartbeatDelegate>
@end

@implementation PlayerDelegate {
}

- (NSTimeInterval) getCurrentPlaybackTime {
    // When called should return the current player time in seconds.
    return playhead_;
}

- (nonnull ADBMediaObject*) getQoSObject {
    // When called should return the latest qos values.
    return qosObject_;
}
@end

ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"app-version";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;
ADBMediaHeartbeatDelegate* delegate = [[PlayerDelegate alloc] init];

ADBMediaHeartbeat* tracker =
  [[ADBMediaHeartbeat alloc] initWithDelegate:delegate config:config];
```

### Launch 拡張機能

[Media API リファレンス - Media Trackerの作成](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createtracker)

トラッカーを作成する前に、メディア拡張機能と依存する拡張機能をモバイルコアに登録します。

```objective-c
// Register the extension once during app launch
#import <ACPCore.h>
#import <ACPAnalytics.h>
#import <ACPMedia.h>
#import <ACPIdentity.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"your-launch-app-id"];
    [ACPMedia registerExtension];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPCore start:nil];
    return YES;
}
```

メディア拡張機能が登録されると、次の API を使用してトラッカーを作成できます。
トラッカーは、設定済みの Launch プロパティから設定を自動的に取得します。

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

## 再生ヘッドと Quality of Experience の値を更新します。

### スタンドアロンの Media SDK

スタンドアロンのMedia SDKでは、デリゲート オブジェクトが
トラッカーの作成中に`ADBMediaHeartbeartDelegate` プロトコルが渡されました。
実装は、常に最新のQoEと再生ヘッドを返す必要があります。
トラッカーは`getQoSObject()`および`getCurrentPlaybackTime()` インターフェイスを呼び出します
方法：

### Launch 拡張機能

実装は、を呼び出して、現在のプレーヤー再生ヘッドを更新する必要があります。
トラッカーにより`updateCurrentPlayhead` メソッドが公開されました。 正確なトラッキングのために
このメソッドは、少なくとも1秒に1回は呼び出す必要があります。

[Media API リファレンス – 現在の再生ヘッドの更新](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#updatecurrentplayhead)

実装は、QoE情報を更新する必要があります。
トラッカーにより`updateQoEObject` メソッドが公開されました。 このメソッドを
品質指標が変更されるたびに確認します。

[Media API リファレンス - QoE オブジェクトの更新](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createqoeobject)

## 標準メディア／広告メタデータを渡す

### スタンドアロンの Media SDK

* 標準メディアメタデータ：

  ```objective-c
  ADBMediaObject *mediaObject =
    [ADBMediaHeartbeat createMediaObjectWithName:@"media-name"
                       mediaId:@"media-id"
                       length:60
                       streamType:ADBMediaHeartbeatStreamTypeVod
                       mediaType:ADBMediaTypeVideo];
  
  // Standard metadata keys provided by adobe.
  NSMutableDictionary *standardMetadata = [[NSMutableDictionary alloc] init];
  [standardMetadata setObject:@"Sample show" forKey:ADBVideoMetadataKeySHOW];
  [standardMetadata setObject:@"Sample season" forKey:ADBVideoMetadataKeySEASON];
  [mediaObject setValue:standardMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
  
  //Attaching custom metadata
  NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
  [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
  [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
  
  [tracker trackSessionStart:mediaObject data:mediaMetadata];
  ```

* 標準の広告メタデータ：

  ```objective-c
  ADBMediaObject* adObject =
    [ADBMediaHeartbeat createAdObjectWithName:[adData objectForKey:@"name"]
                       adId:[adData objectForKey:@"id"]
                       position:[[adData objectForKey:@"position"] doubleValue]
                       length:[[adData objectForKey:@"length"] doubleValue]];
  
  // Standard metadata keys provided by adobe.
  NSMutableDictionary *standardMetadata =
    [[NSMutableDictionary alloc] init];
  [standardMetadata setObject:@"Sample Advertiser"
                    forKey:ADBAdMetadataKeyADVERTISER];
  [standardMetadata setObject:@"Sample Campaign"
                    forKey:ADBAdMetadataKeyCAMPAIGN_ID];
  [adObject setValue:standardMetadata
                    forKey:ADBMediaObjectKeyStandardAdMetadata];
  
  //Attaching custom metadata
  NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
  [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
  
  [tracker trackEvent:ADBMediaHeartbeatEventAdStart
           mediaObject:adObject
           data:adDictionary];
  ```

### Launch 拡張機能

* 標準メディアメタデータ：

  ```objective-c
  NSDictionary *mediaObject =
    [ACPMedia createMediaObjectWithName:@"media-name"
              mediaId:@"media-id"
              length:60
              streamType:ACPMediaStreamTypeVod
              mediaType:ACPMediaTypeVideo];
  
  NSMutableDictionary *mediaMetadata =
    [[NSMutableDictionary alloc] init];
  
  // Standard metadata keys provided by adobe.
  [mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
  [mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];
  
  // Custom metadata keys
  [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
  [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
  [_tracker trackSessionStart:mediaObject data:mediaMetadata];
  ```

* 標準の広告メタデータ：

  ```objective-c
  NSDictionary* adObject =
    [ACPMedia createAdObjectWithName:@"ad-name"
              adId:@"ad-id"
              position:1
              length:15];
  
  NSMutableDictionary* adMetadata =
    [[NSMutableDictionary alloc] init];
  
  // Standard metadata keys provided by adobe.
  [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
  [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];
  
  // Custom metadata keys
  [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];
  
  [tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];
  ```
