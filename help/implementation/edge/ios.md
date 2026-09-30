---
title: ストリーミングメディア用にiOSを設定する
description: IOS上のAdobe Experience Platform Mobile SDKを設定して、ストリーミングメディアデータをEdge Networkに送信します。
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
source-wordcount: '239'
ht-degree: 0%
---
# ストリーミングメディア用にiOSを設定する

Adobe Streaming Media for Edge Network拡張機能（`AEPEdgeMedia`）は、iOSまたはtvOS アプリのメディアセッションデータを収集し、Edge Networkに送信します。 このページでは、コード内の設定について説明します。 代わりにTags モバイルプロパティを使用してSDKを設定するには、「[ タグを使用したストリーミングメディア用にiOSを設定する](ios-tags.md)」を参照してください。

* **前提条件**:
  * [Edgeの実装の概要](overview.md)を完了します（[!UICONTROL Media Analytics]が有効になっているスキーマ、データセット、データストリーム）。
  * アプリに`AEPCore`、`AEPEdge`、`AEPEdgeIdentity`および`AEPEdgeMedia`拡張機能を追加します。 インストールと登録については、[Edge Network用Adobe Streaming Media](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)を参照してください。

## IOS用メディアの設定

SDKを初期化する際に、メディア設定キーを設定します。

```swift
let configuration = [
  "edgeMedia.channel": "sample_channel",
  "edgeMedia.playerName": "player_name",
  "edgeMedia.appVersion": "app_version"
]
MobileCore.updateConfiguration(configuration)
```

次に、メディアセッションを管理するためのトラッカーを作成します。

```swift
let tracker = Media.createTracker()
```

コンフィギュレーションキーと完全なトラッカーAPIについては、[Media for Edge Network API リファレンス ](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/)を参照してください。

## メディアイベントの追跡

トラッカーを作成したら、トラッカーのメソッドを使用して各メディアイベントを追跡します。 正確な呼び出しについては、各[event](/help/implementation/events/overview.md)および[variable](/help/implementation/variables/overview.md) ページの「**iOS**」タブを参照してください。

## 次の手順

実装が完了したら、[Edge実装のレポートを設定できます](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Edge Network用Adobe Streaming Media](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [ タグ付きストリーミングメディア用にiOSを設定](ios-tags.md)
>* [ イベントの概要](/help/implementation/events/overview.md)
