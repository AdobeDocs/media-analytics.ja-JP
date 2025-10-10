---
title: ストリーミングメディア用 Analytics の web 実装をセットアップする方法
description: Web アプリ用の Adobe Streaming Media を実装する方法について説明します。
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 92%

---

# JavaScriptを使用した Media SDKのインストール {#install-web-sdks}

このページの情報では、web スタンドアロン SDK のインストール方法と JavaScript のセットアップ方法について説明します。

または、[Media Analytics 拡張機能を使用したストリーミングメディアサービスのインストール &#x200B;](/help/implementation/media-sdk/setup/web-implementation-tags.md) で説明しているように、Adobe Media Analytics 拡張機能を使用してストリーミングメディアサービスを実装することもできます。

## 前提条件 {#prerequesites}

* **有効な設定パラメーターを取得**

  これらのパラメーターは、Analytics アカウントの設定後、アドビ担当者から取得できます。

* **メディアアプリケーションで JavaScript 用に `AppMeasurement` と `Experience Cloud Identity Service` を実装**

  詳しくは、[JavaScript を使用した Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ja)および [Experience Cloud ID サービスの実装](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=ja)を参照してください。

* **メディアプレーヤーで以下の API を含める**

   * *プレーヤーイベントをサブスクライブするための API* - Media SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - 現在再生中のメディア、広告、チャプターに関する情報が含まれます。

## JavaScript 3.x のセットアップ {#set-up-javascript}

1. [ダウンロードした](/help/getting-started/download-sdks.md)ライブラリをプロジェクトに追加します。利便性のために、クラスへのローカル参照を作成します。

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
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
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

2.x から 3.x への移行について詳しくは、[&#x200B; 2.x から 3.x への移行](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)を参照してください。

レガシーコンテンツについては、[レガシー実装](/help/legacy/media-sdk/setup/setup-overview.md)を参照してください
