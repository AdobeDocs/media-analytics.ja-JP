---
title: ストリーミングメディア用 Analytics用の Web 実装の設定方法
description: Web アプリ用のAdobeストリーミングメディアの実装方法を説明します。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
source-git-commit: d1e7a74a03c68e08987f03a295edc69989d9a4c6
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 69%

---

# JavaScript を使用した Analytics のインストール {#install-web-sdks}

このページの情報では、Web スタンドアロン SDK のインストール方法と JavaScript のセットアップ方法について説明します。

または、 Analytics 拡張機能を使用して、Adobe MediumAnalytics を実装することもできます ( [Media Analytics 拡張機能を使用した Analytics の実装](/help/implementation/media-sdk/setup/web-implementation-tags.md).

## 前提条件 {#prerequesites}

* **有効な設定パラメーターを取得する**

   これらのパラメーターは、Analytics アカウントの設定後、Adobeの担当者から取得できます。

* **実装方法 `AppMeasurement` および `Experience Cloud Identity Service` （メディアアプリケーションの JavaScript 版）**

   詳しくは、 [JavaScript を使用した Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ja) および [Experience CloudID サービスの実装](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=ja).

* **メディアプレーヤーに次の API を含めます**

   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレーヤー情報を提供する API*  — 現在再生中のメディア、広告およびチャプターに関する情報が含まれます。

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

2.x から 3.x への移行について詳しくは、[ 2.x から 3.x への移行](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)を参照してください。

レガシーコンテンツについては、 [レガシー実装](/help/legacy/media-sdk/setup/setup-overview.md)
