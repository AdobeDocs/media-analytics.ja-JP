---
title: タグ付きストリーミングメディア用にiOSを設定する
description: Adobe Streaming Media for Edge Network タグ拡張機能を使用して、iOS用のストリーミングメディア収集を設定します。
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
source-wordcount: '269'
ht-degree: 1%
---
# タグ付きストリーミングメディア用にiOSを設定する

IOSまたはtvOS アプリのストリーミングメディアコレクションは、Tags モバイルプロパティを使用して設定できます。このメディア設定は、Data Collection UIで管理されます。 このページでは、タグ設定について説明します。 代わりにコードでSDKを設定するには、[ ストリーミングメディア用にiOSを設定](ios.md)を参照してください。

* **前提条件**:
  * [Edgeの実装の概要](overview.md)を完了します（[!UICONTROL Media Analytics]が有効になっているスキーマ、データセット、データストリーム）。
  * データ収集UIでモバイルプロパティを作成します。 [Edge Network向けAdobe Streaming Media](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)を参照してください。

## 拡張機能の設定

1. データ収集UIで、モバイルプロパティを開き、**[!UICONTROL 拡張機能]**&#x200B;を選択します。
1. **[!UICONTROL カタログ]** タブで、**Adobe Streaming Media for Edge Network**&#x200B;拡張機能を見つけて、**[!UICONTROL インストール]**&#x200B;を選択します。
1. 以下を設定し、保存します。
   * **[!UICONTROL チャネル]**：各セッションで報告されるチャネル名。
   * **[!UICONTROL Player name]**：使用中のメディアプレーヤーの名前。
   * **[!UICONTROL アプリケーションのバージョン]**：プレーヤーのアプリケーションのバージョン。
1. 変更を公開してから、`AEPCore`、`AEPEdge`、`AEPEdgeIdentity`および`AEPEdgeMedia`の依存関係をアプリに追加し、Mobile Coreに登録します。

## メディアイベントの追跡

プロパティが公開され、トラッカーが作成された状態で、トラッカーメソッドを使用して各メディアイベントを追跡します。 正確な呼び出しについては、各[event](/help/implementation/events/overview.md)および[variable](/help/implementation/variables/overview.md) ページの「**iOS**」タブを参照してください。

## 次の手順

実装が完了したら、[Edge実装のレポートを設定できます](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Edge Network用Adobe Streaming Media](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [ ストリーミングメディア用にiOSを設定する（コード内） ](ios.md)
>* [ イベントの概要](/help/implementation/events/overview.md)
