---
seo-title: JavaScript のセットアップ
title: JavaScript のセットアップ
uuid: 0269d8ad-0af8-4bf1-9d15- e06c2952a005
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# JavaScript のセットアップ{#set-up-javascript}

## 前提条件

* **有効な設定パラメーターの取得**&#x200B;これらのパラメーターは、Analyticsアカウントをセットアップした後、アドビの担当者から取得できます。
* **JavaScript用の実装メディアアプリケーションについ`AppMeasurement`て」を参照してください。Adobe Mobile SDKドキュメントの詳細につい**&#x200B;ては、"JavaScriptを使用したAnalytics [の実装」を参照してください。](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html)

* **メディアプレーヤーで以下の機能を設定します。**

   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - メディア名や再生ヘッドなどの情報がこれに該当します。

1. [ダウンロードした](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211)ライブラリをプロジェクトに追加します。利便性のために、クラスへのローカル参照を作成します。

   1. Expand the `MediaSDK-js-v2.*.zip` file that you downloaded.
   1. Verify that the `MediaSDK.min.js` file exists in the `libs` directory:

   1. Host the `MediaSDK.min.js` file.

      このコア JavaScript ファイルは、サイトのすべてのページから参照可能な Web サーバーでホストする必要があります。次の手順で、これらのファイルへのパス情報が必要になります。

   1. サイトのすべてのページから `MediaSDK.min.js` を参照します。

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. 次に例を示します。

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1.  ライブラリが正しくインポートされたことをすばやく確認するには、`ADB.va.MediaHeartbeatConfig` クラスをインスタンス化します。

      >[!NOTE]
      >
      >From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders.

1. API に簡単にアクセスできるように、`MediaHeartbeat` クラスへのローカル参照を作成します。

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. `MediaHeartbeatConfig` インスタンスを作成します。

   ここでは、`MediaHeartbeat` 設定パラメーターと、正確な追跡のために `MediaHeartbeat` インスタンスに正しい設定値を設定する方法について説明します。

   `MediaHeartbeatConfig` 初期化のサンプル：

   ```js
   //Media Heartbeat initialization 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
   mediaConfig.playerName = Configuration.PLAYER.NAME; 
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
   ```

1. `MediaHeartbeatDelegate` プロトコルを実装します。

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Replace <currentPlaybackTime> with the video player current playback time 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return <currentPlaybackTime>; 
   }; 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>); 
   };
   ```

1. `MediaHeartbeat` インスタンスを作成します。

   Use the `MediaHeartbeatConfig` and `MediaHeartbeatDelegate` to create the `MediaHeartbeat` instance.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the media session. このインスタンスは、以下のすべてのトラッキングイベントに使用されます。

   >[!TIP]
   >
   >`MediaHeartbeat` には、Adobe `AppMeasurement` Analyticsに呼び出しを送信するためのインスタンスが必要です。以下に、`AppMeasurement` インスタンスの例を示します。

   ```js
   var appMeasurement = new AppMeasurement(); 
   appMeasurement.visitor = visitor; 
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
   appMeasurement.account = <rsid>; 
   appMeasurement.pageName = <page_name>; 
   appMeasurement.charSet = "UTF­8";
   ```

## JavaScript でのバージョン 1.x から 2.x への移行

バージョン 2.x では、すべてのパブリックメソッドは、開発をより簡単にするために、`ADB.va.MediaHeartbeat` クラスに統合されています。また、すべての設定は、`ADB.va.MediaHeartbeatConfig` クラスに統合されました。

For detailed information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
