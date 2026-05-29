---
title: ストリーミングメディア用 Analytics の web 実装をセットアップする方法
description: Web アプリ用の Adobe Streaming Media を実装する方法について説明します。
feature: Streaming Media
role: User, Admin, Developer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
TQID: https://experienceleague.adobe.com/UBY26SeGZbGWHjwOm6-YZNET8fe5Gvvco7aIZ9Z7rZg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 78%

---

# JavaScriptを使用したMedia SDKのインストール {#install-web-sdks}

>[!IMPORTANT]
>
>ここでは、AnalyticsのみのJavaScript Web SDKの実装について説明します。 推奨される実装については、[Edge Networkを使用したストリーミングメディアの実装](/help/implementation/edge/edge-web-sdk.md)を参照してください。

このページの情報では、web スタンドアロン SDK のインストール方法と JavaScript のセットアップ方法について説明します。

または、[Media Analytics拡張機能を使用したストリーミングメディアサービスのインストール &#x200B;](/help/implementation/media-sdk/setup/web-implementation-tags.md)で説明しているように、Adobe Media Analytics拡張機能を使用してストリーミングメディアサービスを実装することもできます。

## 前提条件 {#prerequesites}

* **有効な設定パラメーターの取得**

  これらのパラメーターは、Analytics アカウントの設定後、アドビ担当者から取得できます。

* **メディアアプリケーションで JavaScript 用に `AppMeasurement` と `Experience Cloud Identity Service` を実装**

  詳しくは、[AppMeasurementを使用したAnalyticsの実装](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ja)および[JavaScriptを使用した訪問者特定](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/appmeasurement)を参照してください。

* **メディアプレーヤーで以下の API を含める**

   * *プレーヤーイベントをサブスクライブするための API* - Media SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API* - 現在再生中のメディア、広告、チャプターに関する情報が含まれます。

## JavaScript 3.x のセットアップ {#set-up-javascript}

1. [ダウンロードした](/help/getting-started/download-sdks.md)ライブラリをプロジェクトに追加します。 利便性のために、クラスへのローカル参照を作成します。

   1. ダウンロードした `MediaSDK-js-v3*.zip` ファイルを展開します。
   1. `libs` ディレクトリに `MediaSDK.js` ファイルが存在することを確認します。

   1. `MediaSDK.js` ファイルをホストします。

      このコア JavaScript ファイルは、サイトのすべてのページから参照可能な Web サーバーでホストする必要があります。 次の手順で、これらのファイルへのパス情報が必要になります。

   1. サイトのすべてのページから `MediaSDK.js` を参照します。

      各ページの `<head>` タグまたは `<body>` タグに以下のコードを追加して、JavaScript 用の `MediaSDK` を含めます。 次に例を示します。

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
   >`tracker` インスタンスがアクセス可能であることと、メディアセッションの終わりまで解放されないことを確認します。 このインスタンスは、そのセッションで、その後のイベントをすべて追跡するために使用されます。

## JavaScript 2.x から 3.x への移行

2.xから3.xへの移行について詳しくは、[JS SDK 2.xから3.x](/help/implementation/media-sdk/setup/migrate-js-2x-to-3x.md)への移行を参照してください。
