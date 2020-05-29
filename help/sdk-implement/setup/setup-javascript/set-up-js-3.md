---
title: JavaScript 3.xの設定
description: JavaScript 3.xでの実装用のメディアSDKアプリケーション設定。
translation-type: tm+mt
source-git-commit: b642bd1a136e62901847f2a8cf004d05282fca01
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 47%

---


# JavaScript 3.xの設定{#set-up-javascript}

## 前提条件

* **有効な設定パラメーターを取得** これらのパラメーターは、Analytics アカウントの設定後、アドビの担当者から取得できます。
* **メディアアプリケーション`AppMeasurement`にJavaScript`Experience Cloud Identity Service`とJavaScriptを実装します**。詳しくは、AnalyticsのJavaScriptを使用した実装 [およびExperience Cloud Identityサービスの](https://docs.adobe.com/content/help/ja-JP/analytics/implementation/js/overview.html)[実装を参照してください。](https://docs.adobe.com/content/help/en/id-service/using/implementation/setup-analytics.html)

* **メディアプレーヤーで以下の機能を設定します。**

   * *プレーヤーイベントをサブスクライブするための API* - メディア SDK では、プレーヤーでイベントが発生する際に、シンプルな API のセットを呼び出す必要があります。
   * *プレイヤー情報を提供するAPI* — これには、現在再生中のメディア、広告、チャプターに関する情報が含まれます。

1. [ダウンロードした](/help/sdk-implement/download-sdks.md#download-3x-sdks)ライブラリをプロジェクトに追加します。利便性のために、クラスへのローカル参照を作成します。

   1. ダウンロードした `MediaSDK-js-v3*.zip` ファイルを展開します。
   1. `libs` ディレクトリに `MediaSDK.js` ファイルが存在することを確認します。

   1. `MediaSDK.js` ファイルをホストします。

      このコア JavaScript ファイルは、サイトのすべてのページから参照可能な Web サーバーでホストする必要があります。次の手順で、これらのファイルへのパス情報が必要になります。

   1. サイトのすべてのページから `MediaSDK.js` を参照します。

      各ページの `<head>` タグまたは `<body>` タグに以下のコードを追加して、JavaScript 用の `MediaSDK` を含めます。例：

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. ライブラリが正常に読み込まれたことをすばやく確認するには、Windowオブジェクトにチェック `ADB.Media` を書き出します。

      >[!NOTE]
      >
      >The JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `MediaSDK.js` can also be used with compatible module loaders.

1. のインスタンスを作成し、 `AppMeasurement` 設定を行い `visitor`ます。

   メディアSDKの設定には、が設定されたのインスタンス `AppMeasurement` が必要 `visitor` です。

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. メディアSDKの設定

   メディアSDKは、Webページごとに1回設定する必要があります。設定は、作成されるすべてのトラッカーインスタンスに適用されます。

   >[!IMPORTANT]
   >
   > Media SDK(3.x)は、2.x SDKで使用されているHBエンドポイントとは異なるメディアの追跡に、Media Collection APIを使用します。 詳細については、アドビの担当者にお問い合わせください。

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

   メディアSDKの設定後、メディアコンテンツを追跡するためのトラッカーインスタンスを `getInstance` APIを使用して作成できます。

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >`tracker` インスタンスがアクセス可能であることと、メディアセッションの終わりまで解放されないことを確認します。このインスタンスは、そのセッションの以下のイベントをすべて追跡するために使用されます。

## JavaScript 2.xから3.xへの移行

2.x から 3.x への移行について詳しくは、[ 2.x から 3.x への移行](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)を参照してください。
