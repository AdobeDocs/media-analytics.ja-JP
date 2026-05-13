---
title: スタンドアロン Media SDKからAdobe Launchへの移行 – Android
description: Media SDK から Android 用の Launch に移行する方法を説明します。
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/HawnzTGV1nsGCibAtXkl3cAB5NjO2VfUpQODm6-w-qk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 428
ht-degree: 48%

---

# スタンドアロンの Media SDK から Adobe Launch への移行 - Android

>[!NOTE]
>Adobe Experience Platform Launch は、Experience Platform のデータ収集テクノロジースイートとしてリブランドされています。 その結果、製品ドキュメント全体でいくつかの用語の変更がロールアウトされました。 用語の変更点の一覧については、次の[ドキュメント](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ja)を参照してください。


## 設定

### スタンドアロンの Media SDK

スタンドアロン Media SDKでは、アプリでトラッキングを設定し、に渡します
SDKを使います。

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

1. Experience Platform Launchで、[!UICONTROL 拡張機能] タブをクリックします
モバイルプロパティ：
1. 「[!UICONTROL  カタログ ]」タブで、Adobe Media Analytics for Audioを探します
ビデオ拡張機能を追加し、[!UICONTROL  インストール ]をクリックします。
1. 拡張機能の設定ページで、トラッキングパラメーターを設定します。
メディア拡張機能では、設定済みのパラメーターをトラッキングに使用します。

![](assets/launch_config_mobile.png)

[モバイル拡張機能の使用](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

## トラッカーの作成

### スタンドアロンの Media SDK

スタンドアロン Media SDKでは、`MediaHeartbeatConfig` オブジェクトを手動で作成します
トラッキングパラメーターを設定します。 デリゲート インターフェイスを実装して、公開する
`getQoSObject()`および `getCurrentPlaybackTime()functions.`
トラッキング用の`MediaHeartbeat` インスタンスを作成します。

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

[Media API リファレンス - Media Trackerの作成](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createtracker)

トラッカーを作成する前に、メディア拡張機能と
モバイルコアを備えた依存する拡張機能。

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

メディア拡張機能を登録したら、次の API を使用してトラッカーを作成します。
トラッカーは、設定済みの Launch プロパティから設定を自動的に取得します。

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

スタンドアロンのMedia SDKでは、デリゲート オブジェクトを渡して、
トラッカーの作成中に`MediaHeartbeartDelegate` インターフェイスを使用します。  導入プロセス
トラッカーが呼び出すたびに、最新のQoEと再生ヘッドを返す必要があります
`getQoSObject()`および`getCurrentPlaybackTime()` インターフェイス メソッド。

### Launch 拡張機能

実装は、現在のプレーヤー再生ヘッドを更新するには、を呼び出します。
トラッカーにより`updateCurrentPlayhead` メソッドが公開されました。 正確なトラッキングのために
このメソッドは、少なくとも1秒に1回は呼び出す必要があります。

[Media API リファレンス – 現在のプレーヤーを更新](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#updatecurrentplayhead)

実装は、QoE情報を更新する必要があります。 `updateQoEObject`
トラッカーによって公開されたメソッド。 このメソッドは、常にそこにあるときに呼び出されることを期待します
品質指標の変更です。

[Media API リファレンス - QoE オブジェクトの更新](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createqoeobject)

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
