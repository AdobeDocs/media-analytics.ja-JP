---
title: ストリーミングメディア用のWeb SDK タグ拡張機能の設定
description: Adobe Experience Platform Web SDK タグ拡張機能でストリーミングメディアコレクションを設定します。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# ストリーミングメディア用のWeb SDK タグ拡張機能の設定

Adobe Experience Platform Web SDK タグ拡張機能を使用すると、データ収集UIで`alloy.js`設定コードを使用せずにストリーミングメディアコレクションを設定できます。 このページでは、タグ設定について説明します。 代わりにコードでWeb SDKを設定するには、[ ストリーミングメディア用のWeb SDKの設定](web-sdk.md)を参照してください。

* **前提条件**:
   * [Edgeの実装の概要](overview.md)を完了します（[!UICONTROL Media Analytics]が有効になっているスキーマ、データセット、データストリーム）。
   * Web SDK タグ拡張機能をインストールして設定します。 [Web SDK タグ拡張機能の概要](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)を参照してください。

## 拡張機能でのストリーミングメディアの設定

1. データ収集UIでweb プロパティを開き、**[!UICONTROL 拡張機能]**&#x200B;を選択します。
1. インストール済みの&#x200B;**Adobe Experience Platform Web SDK**&#x200B;拡張機能で、**[!UICONTROL Configure]**&#x200B;を選択します。
1. 「**[!UICONTROL ストリーミングメディア]**」セクションを展開し、次のように設定します。
   * **[!UICONTROL Channel]** – 各セッションで報告されるチャネル名。
   * **[!UICONTROL Player name]** – 使用中のメディアプレーヤーの名前。
   * **[!UICONTROL アプリケーションのバージョン]** — Player アプリケーションのバージョン。
   * **[!UICONTROL メイン ping インターバル]**&#x200B;および&#x200B;**[!UICONTROL Ad ping インターバル]** — メインコンテンツと広告のping ケイデンス （秒単位）。
1. 拡張機能の設定を保存し、変更を公開します。

## メディアイベントの追跡

拡張機能を設定した状態で、**[!UICONTROL イベントを送信]** アクション（または`sendEvent` コマンド）を使用して各メディアイベントを送信します。 正確なペイロードについては、各[event](/help/implementation/events/overview.md)および[variable](/help/implementation/variables/overview.md) ページの「**Web SDK**」タブを参照してください。

## 次の手順

実装が完了したら、[Edge実装のレポートを設定できます](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Web SDK タグ拡張機能の概要](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)
>* [ ストリーミングメディア用のWeb SDKの設定（コード内） ](web-sdk.md)
>* [ イベントの概要](/help/implementation/events/overview.md)
