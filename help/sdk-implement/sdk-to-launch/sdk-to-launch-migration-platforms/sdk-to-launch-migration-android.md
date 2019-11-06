---
seo-title: スタンドアロンのメディアSDKからAdobe Launchへの移行 — Android
title: スタンドアロンのメディアSDKからAdobe Launchへの移行 — Android
seo-description: Media SDKからLaunch for Androidへの移行に役立つ手順とコードサンプルです。
description: Media SDKからLaunch for Androidへの移行に役立つ手順とコードサンプルです。
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# スタンドアロンのメディアSDKからAdobe Launchへの移行 — Android

## 設定

### Launch Extension

1. 「エクスペリエンスプラットフォームの起動」で、 [!UICONTROL mobileプロパティの] 「拡張」タブをクリックします。
1. 「カタログ [!UICONTROL 」タブで] 、オーディオおよびビデオ用Adobe Media Analyticsの拡張機能を探し、「インストール」をクリック [!UICONTROL します]。
1. 拡張機能の設定ページで、トラッキングパラメーターを設定します。
メディア拡張では、設定済みのパラメーターをトラッキングに使用します。

[Mobile Extensionsの使用](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

### スタンドアロンメディアSDK

スタンドアロンのメディアSDKでは、アプリでトラッキングを設定し、トラッカーを作成する際にSDKに渡します。

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

## トラッカーの作成

### Launch Extension

[メディアAPIリファレンス — メディアトラッカーの作成](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

トラッカーを作成する前に、メディア拡張と依存する拡張をモバイルコアに登録する必要があります。

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

メディア拡張機能を登録したら、次のAPIを使用してトラッカーを作成します。
トラッカーは、設定された起動プロパティから設定を自動的に選択します。

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

### スタンドアロンメディアSDK

スタンドアロンのメディアSDKでは、オブジェクトを手動で作成し、ト `MediaHeartbeatConfig` ラッキングパラメーターを設定します。 delegateインターフェイスを実装し、トラッキ`getQoSObject()` ング用のイン `getCurrentPlaybackTime()functions.``MediaHeartbeat` スタンスを作成します。

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

## 再生ヘッドとエクスペリエンスの質の値を更新しています。

### Launch Extension

実装では、トラッカーによって公開されたメソッドを呼び出して`updateCurrentPlayhead` 、現在のプレーヤー再生ヘッドを更新する必要があります。 正確な追跡を行うには、このメソッドを少なくとも1秒に1回呼び出す必要があります。

[メディアAPIリファレンス — 現在のプレイヤーを更新](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

実装では、トラッカーが公開するメソッドを呼び出してQoE `updateQoEObject`情報を更新する必要があります。 品質指標に変更が生じた場合は常に、このメソッドが呼び出されることを期待しています。

[メディアAPIリファレンス — qoEオブジェクトの更新](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

### スタンドアロンメディアSDK

スタンドアロンのMedia SDKでは、トラッカーの作成中にインターフェイスを実装するdelegate`MediaHeartbeartDelegate` オブジェクトを渡します。  トラッカーがインターフェイスメソッドおよびインターフェイスメソッドを呼び出すたびに`getQoSObject()` 、実装は最新のQoEと再生ヘッド `getCurrentPlaybackTime()` を返す必要があります。

## 標準メディア/広告メタデータを渡す

### Launch Extension

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

* 標準の広告メタデータ:

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

### スタンドアロンメディアSDK

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

* 標準の広告メタデータ:

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


