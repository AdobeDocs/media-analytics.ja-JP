---
title: ストリーミングメディア用にJavaScriptを設定する
description: Analyticsのみのストリーミングメディア実装用JavaScript用Media SDK（3.x）をインストールして設定します。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 3%
---
# ストリーミングメディア用にJavaScriptを設定する

Media SDK for JavaScript（3.x）は、ストリーミングメディアデータをAdobe Analyticsに直接送信します。 このページでは、JavaScriptの手動インストールについて説明します。 代わりにタグを使用してSDKをデプロイするには、[Media Analytics タグ拡張機能の設定](javascript-tags.md)を参照してください。 新しい実装の場合は、[Web SDK](/help/implementation/edge/web-sdk.md)を使用して、Edge Network データストリームを介してAdobe Analyticsにデータを送信することを検討してください。

* **前提条件**:
  * [Analyticsのみの実装の概要](overview.md)を完了します。
  * [AppMeasurement](https://experienceleague.adobe.com/ja/docs/analytics/implementation/js/overview)と[訪問者ID サービス &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/appmeasurement)を実装します。
  * [JavaScript用Media SDKをダウンロード &#x200B;](/help/getting-started/download-sdks.md)。

## SDKのインストールと設定

1. （ダウンロードした`libs` ディレクトリから）すべてのページにアクセス可能なweb サーバーに`MediaSDK.js`をホストし、各ページで参照します。

   ```html
   <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH/MediaSDK.js"></script>
   ```

1. ページごとに1回Media SDKを設定し、前提条件として設定した`appMeasurement` インスタンスを渡します。

   ```js
   var mediaConfig = new ADB.MediaConfig();
   mediaConfig.trackingServer = "<media_collection_server>";
   mediaConfig.playerName = "player_name";
   mediaConfig.channel = "sample_channel";
   mediaConfig.appVersion = "app_version";
   mediaConfig.ssl = true;
   
   ADB.Media.configure(mediaConfig, appMeasurement);
   ```

   >[!NOTE]
   >
   >`mediaConfig.trackingServer`変数は&#x200B;**メディアコレクションサーバー** （例：`[namespace].hb-api.omtrdc.net`）です。 このコレクションサーバーは、AppMeasurement インスタンス内で設定されたAnalytics トラッキングサーバーとは異なります。

1. `getInstance`でトラッカーインスタンスを作成します。 メディアセッション全体でインスタンスにアクセスできるようにします。

   ```js
   var tracker = ADB.Media.getInstance();
   ```

## メディアイベントの追跡

トラッカーを作成したら、トラッカーのメソッドを使用して各メディアイベントを追跡します。 正確な呼び出しについては、各[event](/help/implementation/events/overview.md)および[variable](/help/implementation/variables/overview.md) ページの&#x200B;**Media SDK JS 3.x** タブを参照してください。

## 次の手順

実装が完了したら、[Analyticsのみの実装用のレポートを設定できます](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [JavaScript 3.x用Media SDK API リファレンス &#x200B;](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md)
>* [JS SDK 2.xから3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/MigrationGuide.md)への移行
>* [Media Analytics タグ拡張機能の設定](javascript-tags.md)
>* [&#x200B; イベントの概要](/help/implementation/events/overview.md)
