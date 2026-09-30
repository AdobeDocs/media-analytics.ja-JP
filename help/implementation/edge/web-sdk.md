---
title: ストリーミングメディア用のWeb SDKの設定
description: Adobe Experience Platform Web SDK（alloy.js）を設定して、ストリーミングメディアデータをEdge Networkに送信します。
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
source-wordcount: '283'
ht-degree: 5%
---
# ストリーミングメディア用のWeb SDKの設定

Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview) （`alloy.js`、バージョン 2.20.0以降）の`streamingMedia` コンポーネントは、web サイト上のメディアセッションデータを収集し、それをEdge Networkに送信します。 このページでは、インコード （`alloy.js`）設定について説明します。 代わりにタグを使用してWeb SDKを設定するには、[ ストリーミングメディア用のWeb SDK タグ拡張機能の設定](web-sdk-tags.md)を参照してください。

* **前提条件**:
  * [Edgeの実装の概要](overview.md)を完了します（[!UICONTROL Media Analytics]が有効になっているスキーマ、データセット、データストリーム）。
  * Web SDK 2.20.0以降をインストールします。 [Web SDKのインストール ](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/install/overview)を参照してください。

## streamingMedia コンポーネントの設定

`streamingMedia` コンポーネントを`alloy`設定に追加します。

```js
alloy("configure", {
  edgeConfigId: "<datastreamID>",
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

構成の詳細については、[`streamingMedia` コマンド ](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia)を参照してください。

### Media JS SDKからの移行

Media JS （3.x） SDKから移行する場合、Web SDK [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/getmediaanalyticstracker) コマンドは、[3.x Media SDK](/help/implementation/analytics-only/javascript.md)と同じAPIを公開するトラッカーインスタンスを返すため、既存のトラッキング呼び出しは引き続き機能します。

## メディアイベントの追跡

SDKが設定された状態で、[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を呼び出して各メディアイベントを送信します。 正確なペイロードについては、各[event](/help/implementation/events/overview.md)および[variable](/help/implementation/variables/overview.md) ページの「**Web SDK**」タブを参照してください。

## 次の手順

実装が完了したら、[Edge実装のレポートを設定できます](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Web SDK の概要](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview)
>* [ イベントの概要](/help/implementation/events/overview.md)
>* [変数の概要](/help/implementation/variables/overview.md)
