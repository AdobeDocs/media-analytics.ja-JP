---
title: JavaScript 2.x を使用して Media SDK をセットアップする方法
description: JavaScript 2.x で Media SDK アプリケーションをセットアップするには、次の手順に従います。
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mYfKt95xUE59MuMFOzGro6fPsJsdy4wcy2F2J--JaW8
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 89%

---

# JavaScript 2.x のセットアップ{#set-up-javascript}

## 前提条件

* **有効な設定パラメーターの取得**
これらのパラメーターは、analytics アカウントを設定した後で、Adobe担当者から取得できます。
* **メディアアプリケーションでJavaScriptの`AppMeasurement`を実装する**
Adobe Mobile SDKのドキュメントについて詳しくは、[JavaScriptを使用したAnalyticsの実装](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ja)を参照してください。

* **メディアプレーヤーで以下の機能を設定します。**

   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - メディア名や再生ヘッドなどの情報がこれに該当します。

1. [ダウンロードした](/help/getting-started/download-sdks.md)ライブラリをプロジェクトに追加します。 利便性のために、クラスへのローカル参照を作成します。

   1. ダウンロードした `MediaSDK-js-v2.*.zip` ファイルを展開します。
   1. `libs` ディレクトリに `MediaSDK.min.js` ファイルが存在することを確認します。

   1. `MediaSDK.min.js` ファイルをホストします。

      このコア JavaScript ファイルは、サイトのすべてのページから参照可能な Web サーバーでホストする必要があります。 次の手順で、これらのファイルへのパス情報が必要になります。

   1. サイトのすべてのページから `MediaSDK.min.js` を参照します。

      各ページの `<head>` タグまたは `<body>` タグに以下のコードを追加して、JavaScript 用の `MediaSDK` を含めます。 次に例を示します。

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. ライブラリが正しくインポートされたことをすばやく確認するには、`ADB.va.MediaHeartbeatConfig` クラスをインスタンス化します。

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
   >`MediaHeartbeat` インスタンスがアクセス可能であることと、メディアセッションの終わりまで解放されないことを確認します。 このインスタンスは、以下のすべてのトラッキングイベントに使用されます。

   >[!TIP]
   >
   >`MediaHeartbeat` が Adobe Analytics に呼び出しを送信するためには、`AppMeasurement` のインスタンスが必要です。 以下に、`AppMeasurement` インスタンスの例を示します。

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## JavaScript 1.x から 2.x への移行

バージョン 2.x では、すべてのパブリックメソッドは、開発をより簡単にするために、`ADB.va.MediaHeartbeat` クラスに統合されています。 また、すべての設定は、`ADB.va.MediaHeartbeatConfig` クラスに統合されました。

1.x から 2.x への移行について詳しくは、レガシー実装のドキュメントを参照してください。
