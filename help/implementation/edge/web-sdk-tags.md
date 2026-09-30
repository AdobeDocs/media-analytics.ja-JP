---
title: ストリーミングメディア用のWeb SDK タグ拡張機能の設定
description: Adobe Experience Platform Web SDK タグ拡張機能でストリーミングメディアコレクションを設定します。
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
source-wordcount: '286'
ht-degree: 0%
---
# ストリーミングメディア用のWeb SDK タグ拡張機能の設定

Adobe Experience Platform Web SDK タグ拡張機能を使用すると、データ収集UIで`alloy.js`設定コードを使用せずにストリーミングメディアコレクションを設定できます。 このページでは、タグ設定について説明します。 代わりにコードでWeb SDKを設定するには、[&#x200B; ストリーミングメディア用のWeb SDKの設定](web-sdk.md)を参照してください。

* **前提条件**:
  * [Edgeの実装の概要](overview.md)を完了します（[!UICONTROL Media Analytics]が有効になっているスキーマ、データセット、データストリーム）。
  * Web SDK タグ拡張機能をインストールして設定します。 [Web SDK タグ拡張機能の概要](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)を参照してください。

## 拡張機能でのストリーミングメディアの設定

1. データ収集UIでweb プロパティを開き、**[!UICONTROL 拡張機能]**&#x200B;を選択します。
1. インストール済みの&#x200B;**Adobe Experience Platform Web SDK**&#x200B;拡張機能で、**[!UICONTROL Configure]**&#x200B;を選択します。
1. 「**[!UICONTROL ストリーミングメディア]**」セクションを展開し、次のように設定します。
   * **[!UICONTROL チャネル]**：各セッションで報告されるチャネル名。
   * **[!UICONTROL Player name]**：使用中のメディアプレーヤーの名前。
   * **[!UICONTROL アプリケーションのバージョン]**：プレーヤーのアプリケーションのバージョン。
   * **[!UICONTROL メインのping間隔]**&#x200B;と&#x200B;**[!UICONTROL 広告のping間隔]**：メインコンテンツと広告のping頻度（秒単位）。
1. 拡張機能の設定を保存し、変更を公開します。

## メディアイベントの追跡

拡張機能を設定した状態で、**[!UICONTROL イベントを送信]** アクション（または`sendEvent` コマンド）を使用して各メディアイベントを送信します。 正確なペイロードについては、各[event](/help/implementation/events/overview.md)および[variable](/help/implementation/variables/overview.md) ページの「**Web SDK**」タブを参照してください。

## 次の手順

実装が完了したら、[Edge実装のレポートを設定できます](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Web SDK タグ拡張機能の概要](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)
>* [&#x200B; ストリーミングメディア用のWeb SDKの設定（コード内） &#x200B;](web-sdk.md)
>* [&#x200B; イベントの概要](/help/implementation/events/overview.md)
