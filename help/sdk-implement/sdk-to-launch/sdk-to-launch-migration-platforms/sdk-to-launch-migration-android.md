---
title: 「スタンドアロンのメディアSDKからAdobeLaunchへの移行 — Android」
description: メディアSDKからLaunch for Androidに移行する方法を説明します。
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 93%

---

# スタンドアロンの Media SDK から Adobe Launch への移行 - Android

## 設定

### スタンドアロンの Media SDK

スタンドアロンの Media SDK では、アプリケーションでトラッキングを設定し、トラッカーを作成する際に SDK に渡します。

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeat tracker = new MediaHeartbeat(... , config);
```

### Launch 拡張機能

1. Experience Platform Launch でモバイルプロパティの「[!UICONTROL 拡張機能]」タブをクリックします。
1. 「[!UICONTROL カタログ]」タブでオーディオおよびビデオ用 Adobe Media Analytics 拡張機能を探し、「[!UICONTROL インストール]」をクリックします。
1. 拡張機能の設定ページで、トラッキングパラメーターを設定します。メディア拡張機能では、設定済みのパラメーターをトラッキングに使用します。

![](assets/launch_config_mobile.png)

[モバイル拡張機能の使用](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## トラッカーの作成

### スタンドアロンの Media SDK

スタンドアロンのメディア SDK では、`MediaHeartbeatConfig` オブジェクトを手動で作成し、トラッキングパラメーターを設定します。`getQoSObject()` および `getCurrentPlaybackTime()functions.` を公開する delegate インターフェイスを実装し、トラッキング用の `MediaHeartbeat` インスタンスを作成します。

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeatDelegate delegate = new MediaHeartbeatDelegate() {
    @Override 
    public MediaObject getQoSObject() {
        // When called should return the latest qos values.
        return MediaHeartbeat.createQoSObject(<bitrate>,  
                                              <startupTime>,  
                                              <fps>,  
                                              <droppedFrames>); 
    } 

    @Override 
    public Double getCurrentPlaybackTime() { 
        // When called should return the current player time in seconds.
        return <currentPlaybackTime>; 
    }

    MediaHeartbeat tracker = new MediaHeartbeat(delegate, config);
}
```

### Launch 拡張機能

[メディア API リファレンス - メディアトラッカーの作成](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

トラッカーを作成する前に、メディア拡張機能と依存する拡張機能をモバイルコアに登録する必要があります。

```java
// Register the extension once during app launch
try {
    // Media needs Identity and Analytics extension 
    // to function properly
    Identity.registerExtension();
    Analytics.registerExtension();

    // Initialize media extension.
    Media.registerExtension();                
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            // Launch mobile property to pick extension settings.
            MobileCore.configureWithAppID("LAUNCH_MOBILE_PROPERTY");
        }
    });
} catch (InvalidInitException ex) {
    ...
}
```

メディア拡張機能を登録したら、次の API を使用してトラッカーを作成します。トラッカーは、設定済みの Launch プロパティから設定を自動的に取得します。

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

## 再生ヘッドと Quality of Experience の値を更新します。

### スタンドアロンの Media SDK

スタンドアロンの Media SDK では、トラッカーの作成中に `MediaHeartbeartDelegate` インターフェイスを実装する delegate オブジェクトを渡します。トラッカーが `getQoSObject()` および `getCurrentPlaybackTime()` インターフェイスメソッドを呼び出すたびに、実装は最新の QoE と再生ヘッドを返す必要があります。

### Launch 拡張機能

実装では、トラッカーによって公開された `updateCurrentPlayhead` メソッドを呼び出して、現在のプレーヤーの再生ヘッドを更新する必要があります。正確な追跡をおこなうには、このメソッドを少なくとも 1 秒に 1 回呼び出す必要があります。

[メディア API リファレンス - 現在のプレーヤーを更新](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

実装では、トラッカーによって公開された `updateQoEObject` メソッドを呼び出して QoE 情報を更新する必要があります。品質指標に変更が生じた場合は常に、このメソッドが呼び出されることを想定しています。

[メディア API リファレンス - QoE オブジェクトの更新](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## 標準メディア／広告メタデータを渡す

### スタンドアロンの Media SDK

* 標準メディアメタデータ：

   ```java
   MediaObject mediaInfo = 
     MediaHeartbeat.createMediaObject("media-name", 
                                      "media-id", 
                                      60D, 
                                      MediaHeartbeat.StreamType.VOD, 
                                      MediaHeartbeat.MediaType.Video);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardVideoMetadata = 
     new HashMap<String, String>(); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, 
                             "Sample Episode"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, 
                             "Sample Show"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, 
                             "Sample Season"); 
   mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata, 
                      standardVideoMetadata);
   
   // Custom metadata keys
   HashMap<String, String> mediaMetadata = new HashMap<String, String>();
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* 標準の広告メタデータ：

   ```java
   MediaObject adInfo = 
     MediaHeartbeat.createAdObject("ad-name", 
                                   "ad-id", 
                                   1L, 
                                   15D);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardAdMetadata = 
     new HashMap<String, String>(); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, 
                          "Sample Advertiser"); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, 
                          "Sample Campaign"); 
   adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, 
                   standardAdMetadata); 
   
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   
   tracker.trackEvent(MediaHeartbeat.Event.AdStart, 
                      adObject, 
                      adMetadata);
   ```

### Launch 拡張機能

* 標準メディアメタデータ：

   ```java
   HashMap<String, Object> mediaObject = 
     Media.createMediaObject("media-name", 
                             "media-id", 
                             60D, 
                             MediaConstants.StreamType.VOD, 
                             Media.MediaType.Video);
   
   HashMap<String, String> mediaMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE, 
                     "Sample Episode");
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW, 
                     "Sample Show");
   
   // Custom metadata keys
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* 標準の広告メタデータ：

   ```java
   HashMap<String, Object> adObject = 
     Media.createAdObject("ad-name", 
                          "ad-id", 
                          1L, 
                          15D);
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER, 
                  "Sample Advertiser");
   adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID, 
                  "Sample Campaign");
   
   // Custom metadata keys
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   _tracker.trackEvent(Media.Event.AdStart, 
                       adObject, 
                       adMetadata);
   ```
