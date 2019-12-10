---
title: JavaScript のセットアップ
description: JavaScript での実装用のメディア SDK アプリケーション設定です。
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# JavaScript のセットアップ {#set-up-javascript}

## 前提条件

* **有効な設定パラメーターを取得** これらのパラメーターは、Analytics アカウントの設定後、アドビの担当者から取得できます。
* **JavaScript 向け`AppMeasurement`をメディアアプリケーションに実装** Adobe Mobile SDK のドキュメントについて詳しくは、[JavaScript を使用した Analytics の実装](https://marketing.adobe.com/resources/help/ja_JP/sc/implement/js_implementation.html)を参照してください。

* **メディアプレーヤーで以下の機能を設定します。**

   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - メディア名や再生ヘッドなどの情報がこれに該当します。

1. [ダウンロードした](/help/sdk-implement/download-sdks.md#download-2x-sdks)ライブラリをプロジェクトに追加します。利便性のために、クラスへのローカル参照を作成します。

   1. ダウンロードした `MediaSDK-js-v2.*.zip` ファイルを展開します。
   1. `libs` ディレクトリに `MediaSDK.min.js` ファイルが存在することを確認します。

   1. `MediaSDK.min.js` ファイルをホストします。

      このコア JavaScript ファイルは、サイトのすべてのページから参照可能な Web サーバーでホストする必要があります。次の手順で、これらのファイルへのパス情報が必要になります。

   1. サイトのすべてのページから `MediaSDK.min.js` を参照します。

      各ページの `<head>` タグまたは `<body>` タグに以下のコードを追加して、JavaScript 用の `MediaSDK` を含めます。例：

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1.  ライブラリが正しくインポートされたことをすばやく確認するには、`ADB.va.MediaHeartbeatConfig` クラスをインスタンス化します。

      >[!NOTE]
      >
      >バージョン 2.1.0 以降の JavaScript SDK は、AMD および CommonJS モジュールの仕様に準拠しており、互換性のあるモジュールローダーと共に `VideoHeartbeat.min.js` を使用することもできます。

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

   `MediaHeartbeatConfig` および `MediaHeartbeatDelegate` を使用して、`MediaHeartbeat` インスタンスを作成します。

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >`MediaHeartbeat` インスタンスがアクセス可能であることと、メディアセッションの終わりまで解放されないことを確認します。このインスタンスは、以下のすべてのトラッキングイベントに使用されます。

   >[!TIP]
   >
   >`MediaHeartbeat` が Adobe Analytics に呼び出しを送信するためには、`AppMeasurement` のインスタンスが必要です。以下に、`AppMeasurement` インスタンスの例を示します。

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

1.x から 2.x への移行について詳しくは、[VHL 1.x から 2.x への移行](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)を参照してください。
