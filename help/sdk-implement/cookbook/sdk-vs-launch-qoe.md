---
seo-title: 起動とメディアSDKの違いを理解する
title: 起動とメディアSDKの違いを理解する
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# 起動とメディアSDKの違いを理解する

## 機能の違い

* *Launch* - Launchは、Webベースのメディアトラッキングソリューションの設定、設定およびデプロイの手順を示すUIを提供します。 Dynamic Tag Management(DTM)の起動が強化されました。
* *メディアSDK* — メディアSDKは、特定のプラットフォーム向けに設計されたメディアトラッキングライブラリ(例：Android、iOSなど)。 モバイルアプリでのメディア使用状況の追跡には、Media SDKをお勧めします。

## トラッカーの作成の違い

### Launch

Launchは、トラッキングインフラストラクチャを作成する2つの方法を提供します。 どちらの方法でも、Media Analytics Launch Extensionを使用します。

1. WebページからメディアトラッキングAPIを使用します。

   このシナリオでは、Media Analytics Extensionが、グローバルウィンドウオブジェクトの設定済み変数にメディアトラッキングAPIをエクスポートします。

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 別のLaunch拡張からのメディアトラッキングAPIを使用します。

   このシナリオでは、および共有モジュールで公開されているメディアトラッキングAPI `get-instance` を使 `media-heartbeat` 用します。

   >[!NOTE]
   >
   >共有モジュールはWebページでは使用できません。 他の拡張機能の共有モジュールのみを使用できます。

   共有モジュール `MediaHeartbeat` を使用してインスタン `get-instance` スを作成します。
delegateオブジェクトを、公開し `get-instance` たり関数に `getQoSObject()` 渡し `getCurrentPlaybackTime()` ます。

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   共有モジ `MediaHeartbeat` ュールを使用して定数にア `media-heartbeat` クセスします。

### メディア SDK

1. 開発プロジェクトにMedia Analyticsライブラリを追加します。
1. 設定オブジェクトを作成しま`MediaHeartbeatConfig`す()。
1. delegateプロトコルを実装し、関数と関数を `getQoSObject()` 公開 `getCurrentPlaybackTime()` します。
1. Media Heartbeatインスタンスを作成します(`MediaHeartbeat`)。

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

## 関連ドキュメント

### Launch

* [起動の概要](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [MA拡張](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### メディア SDK

* [JSの設定](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

