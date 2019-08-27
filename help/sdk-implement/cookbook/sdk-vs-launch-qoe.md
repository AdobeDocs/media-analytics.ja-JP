---
seo-title: 起動とメディアSDKの違いについて理解する
title: 起動とメディアSDKの違いについて理解する
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# 起動とメディアSDKの違いについて理解する

## 機能の違い

* *Launch* - Launch（起動）- Webベースのメディアトラッキングソリューションの設定、設定およびデプロイに関するUIを提供します。Dynamic Tag Management（DTM）の機能が向上しました。
* *メディアSDK* - Media SDKは、特定のプラットフォーム向けに設計されたメディアトラッキングライブラリを提供します（例:Android、iOSなど）。モバイルアプリでメディアの使用状況を追跡するためのMedia SDKをお勧めします。

## トラッカー作成の違い

### Launch

起動には、トラッキングインフラストラクチャを作成する2つの方法があります。どちらのアプローチでも、Media Analytics Launch Extensionを使用します。

1. WebページのメディアトラッキングAPIを使用します。

   このシナリオでは、Media Analytics Extensionは、メディアトラッキングAPIをグローバルウィンドウオブジェクト内の設定済みの変数にエクスポートします。

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 別の起動拡張機能のメディアトラッキングAPIを使用してください。

   このシナリオでは、共有モジュールによって公開されるメディアトラッキング `get-instance``media-heartbeat` APIを使用します。

   >[!NOTE]
   >
   >共有モジュールはWebページで使用できません。共有モジュールは、別の拡張機能からのみ使用できます。

   共有モジュールを使用して `MediaHeartbeat` インスタンス `get-instance` を作成します。
公開 `get-instance``getQoSObject()` および `getCurrentPlaybackTime()` 機能に委任オブジェクトを渡します。

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   共有モジュールを介して `MediaHeartbeat` 定数 `media-heartbeat` にアクセスします。

### メディア SDK

1. 開発プロジェクトにMedia Analyticsライブラリを追加します。
1. configオブジェクト（`MediaHeartbeatConfig`）を作成します。
1. 委任プロトコルを実装し、関数を公開 `getQoSObject()``getCurrentPlaybackTime()` します。
1. Media Heartbeatインスタンス（`MediaHeartbeat`）を作成します。

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
* [MA Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### メディア SDK

* [JSのセットアップ](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

