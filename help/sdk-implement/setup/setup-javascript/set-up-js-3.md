---
title: JavaScript 3.x を使用して Media SDK をセットアップする方法
description: JavaScript 3.x で Media SDK アプリケーションをセットアップするには、次の手順に従います。
exl-id: 35e27495-e480-4463-9f00-4b60a54d02c1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '405'
ht-degree: 100%

---

# JavaScript 3.x のセットアップ{#set-up-javascript}

## 前提条件 

* **有効な設定パラメーターを取得** これらのパラメーターは、Analytics アカウントの設定後、アドビの担当者から取得できます。
* **メディアアプリケーションで、`AppMeasurement` と JavaScript 向け `Experience Cloud Identity Service` を実装します**。
詳しくは、[JavaScript を使用した Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html) および [Experience Cloud ID サービスの実装](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=ja)を参照してください。

* **メディアプレーヤーで以下の機能を設定します。**

   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - 現在再生中のメディア、広告、チャプターに関する情報が含まれます。

1. [ダウンロードした](/help/sdk-implement/download-sdks.md#download-3x-sdks)ライブラリをプロジェクトに追加します。利便性のために、クラスへのローカル参照を作成します。

   1. ダウンロードした `MediaSDK-js-v3*.zip` ファイルを展開します。
   1. `libs` ディレクトリに `MediaSDK.js` ファイルが存在することを確認します。

   1. `MediaSDK.js` ファイルをホストします。

      このコア JavaScript ファイルは、サイトのすべてのページから参照可能な Web サーバーでホストする必要があります。次の手順で、これらのファイルへのパス情報が必要になります。

   1. サイトのすべてのページから `MediaSDK.js` を参照します。

      各ページの `<head>` タグまたは `<body>` タグに以下のコードを追加して、JavaScript 用の `MediaSDK` を含めます。次に例を示します。

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. ライブラリが正常に読み込まれたことをすばやく確認するには、Window オブジェクトで `ADB.Media` が書き出されていることを確認します。

      >[!NOTE]
      >
      >JavaScript SDK は、AMD および CommonJS モジュールの仕様に準拠しており、互換性のあるモジュールローダーと共に `MediaSDK.js` を使用することもできます。

1. `AppMeasurement` のインスタンスを作成し、`visitor` を設定します。

   メディア SDK の設定には、`visitor` が設定された `AppMeasurement` のインスタンスが必要です。

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. メディア SDK の設定

   メディア SDK は、Web ページごとに 1 回設定する必要があります。設定は、作成されるすべてのトラッカーインスタンスに適用されます。

   >[!IMPORTANT]
   >
   > Media SDK（3.x）は、メディアコレクション API を使用して、2.x SDK で使用されている HB エンドポイントとは異なるメディアを追跡します。詳細については、アドビの担当者にお問い合わせください。

   `MediaConfig` 初期化のサンプル：

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   ```

1. `MediaTracker` インスタンスを作成します。

   メディア SDK の設定後、`getInstance` API を使用して、メディアコンテンツを追跡するためのトラッカーインスタンスを作成できます。

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >`tracker` インスタンスがアクセス可能であることと、メディアセッションの終わりまで解放されないことを確認します。このインスタンスは、そのセッションで、その後のイベントをすべて追跡するために使用されます。

## JavaScript 2.x から 3.x への移行

2.x から 3.x への移行について詳しくは、[ 2.x から 3.x への移行](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)を参照してください。
