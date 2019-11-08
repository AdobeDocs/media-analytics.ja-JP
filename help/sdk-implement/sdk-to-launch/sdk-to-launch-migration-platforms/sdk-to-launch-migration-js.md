---
title: スタンドアロンのメディアSDKからAdobe Launch - Web (JS)への移行
description: Media SDKからLaunchへの移行に役立つ手順とコードサンプルです。
translation-type: tm+mt
source-git-commit: bc896cc403923e2f31be7313ab2ca22c05893c45

---


# スタンドアロンのメディアSDKからAdobe Launch - Web (JS)への移行

## 機能の違い

* *Launch* - Launchは、Webベースのメディアトラッキングソリューションの設定、設定およびデプロイの手順を示すUIを提供します。 Dynamic Tag Management(DTM)の起動が強化されました。
* *メディアSDK* — メディアSDKは、特定のプラットフォーム向けに設計されたメディアトラッキングライブラリ(例：Android、iOSなど)。 モバイルアプリでのメディア使用状況の追跡には、Media SDKをお勧めします。

## 設定

### スタンドアロンメディアSDK

スタンドアロンのメディアSDKでは、アプリでトラッキング設定を設定し、トラッカーの作成時にそれをSDKに渡します。

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

メディアトラッキングが正し `MediaHeartbeat` く機能するには、設定に加えて、ページでインスタンス `AppMeasurement` とインス `VisitorAPI` タンスを設定して渡す必要があります。

### Launch Extension

1. 「エクスペリエンスプラットフォームの起動」で、Webプロパティ [!UICONTROL の「拡張] 」タブをクリックします。
1. 「カタログ [!UICONTROL 」タブで] 、Adobe Media Analytics for Audio andVideo拡張機能を探し、「インストール」をクリック [!UICONTROL します]。
1. 拡張機能の設定ページで、トラッキングパラメーターを設定します。
メディア拡張では、設定済みのパラメーターをトラッキングに使用します。

   ![](assets/launch_config_js.png)

[ユーザーガイドの起動 — メディア拡張のインストールと設定](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## トラッカーの作成の違い

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

[メディアSDK — トラッカーの作成](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html)

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

## 関連ドキュメント

### メディア SDK

* [JSの設定](/help/sdk-implement/setup/set-up-js.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [起動の概要](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Media Analytics Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
