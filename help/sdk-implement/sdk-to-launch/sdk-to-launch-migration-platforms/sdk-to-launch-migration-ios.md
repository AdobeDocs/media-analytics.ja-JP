---
seo-title: スタンドアロンのメディアSDKからAdobe Launchへの移行 — iOS
title: スタンドアロンのメディアSDKからAdobe Launchへの移行 — iOS
seo-description: Media SDKからLaunch for iOSへの移行に役立つ手順とコードサンプルです。
description: Media SDKからLaunch for iOSへの移行に役立つ手順とコードサンプルです。
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# スタンドアロンのメディアSDKからAdobe Launchへの移行 — iOS

## 設定

### Launch Extension

1. 「エクスペリエンスプラットフォームの起動」で、モバイルプロ [!UICONTROL パティの] 「拡張」タブをクリックします
1. 「カタログ [!UICONTROL 」タブで] 、「オーディオ/ビデオ用Adobe Media Analytics」拡張機能を探し、「インストール」をクリック [!UICONTROL します]。
1. 拡張機能の設定ページで、トラッキングパラメーターを設定します。
メディア拡張では、設定済みのパラメーターをトラッキングに使用します。

[Media Analytics拡張の設定](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

### スタンドアロンメディアSDK

スタンドアロンのMedia SDKでは、アプリでトラッキング設定を設定し、トラッカーの作成時にSDKに渡します。

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

## トラッカーの作成

### Launch Extension

[メディアAPIリファレンス — メディアトラッカーを作成](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

トラッカーを作成する前に、メディア拡張と依存する拡張機能をモバイルコアに登録します。

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

メディア拡張機能が登録されると、次のAPIを使用してトラッカーを作成できます。
トラッカーは、設定された起動プロパティから設定を自動的に選択します。

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

### スタンドアロンメディアSDK

スタンドアロンのメディアSDKでは、オブジェクトを手動で作成し、ト `ADBMediaHeartbeatConfig` ラッキングパラメーターを設定します。 delegateインターフェイスを実装し`getQoSObject()` 、 `getCurrentPlaybackTime()functions.`

トラッキング用のMediaHeartbeatインスタンスの作成：

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

## 再生ヘッドとエクスペリエンスの質の値を更新しています。

### Launch Extension

実装では、トラッカーによって公開されたメソッドを呼び出して`updateCurrentPlayhead` 、現在のプレーヤー再生ヘッドを更新する必要があります。 正確な追跡を行うには、このメソッドを少なくとも1秒に1回呼び出す必要があります。

[メディアAPIリファレンス — 現在の再生ヘッドの更新](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

実装では、トラッカーで公開されているメソッドを呼び出して`updateQoEObject` 、QoE情報を更新する必要があります。 品質指標に変更がある場合は常に、このメソッドを呼び出す必要があります。

[メディアAPIリファレンス — qoEオブジェクトの更新](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

### スタンドアロンメディアSDK

スタンドアロンのMedia SDKでは、プロトコルを実装するdelegateオブジェクトが`ADBMediaHeartbeartDelegate` 、トラッカーの作成中に渡されます。
トラッカーがインターフェイスメソッドとインターフェイスメソッドを呼び出すたびに、実装は最新のQoEと再生ヘッド `getQoSObject()` を返す必 `getCurrentPlaybackTime()` 要があります。

## 標準メディア/広告メタデータを渡す

### Launch Extension

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

* 標準の広告メタデータ:

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

### スタンドアロンメディアSDK

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

* 標準の広告メタデータ:

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

