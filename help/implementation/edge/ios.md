---
title: ストリーミングメディア用にiOSを設定する
description: IOS上のAdobe Experience Platform Mobile SDKを設定して、ストリーミングメディアデータをEdge Networkに送信します。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# ストリーミングメディア用にiOSを設定する

Adobe Streaming Media for Edge Network拡張機能（`AEPEdgeMedia`）は、iOSまたはtvOS アプリのメディアセッションデータを収集し、Edge Networkに送信します。 このページでは、コード内の設定について説明します。 代わりにTags モバイルプロパティを使用してSDKを設定するには、「[&#x200B; タグを使用したストリーミングメディア用にiOSを設定する](ios-tags.md)」を参照してください。

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

コンフィギュレーションキーと完全なトラッカーAPIについては、[Media for Edge Network API リファレンス &#x200B;](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/)を参照してください。

## メディアイベントの追跡

トラッカーを作成したら、トラッカーのメソッドを使用して各メディアイベントを追跡します。 正確な呼び出しについては、各[event](/help/implementation/events/overview.md)および[variable](/help/implementation/variables/overview.md) ページの「**iOS**」タブを参照してください。

## 次の手順

実装が完了したら、[Edge実装のレポートを設定できます](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Edge Network用Adobe Streaming Media](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [&#x200B; タグ付きストリーミングメディア用にiOSを設定](ios-tags.md)
>* [&#x200B; イベントの概要](/help/implementation/events/overview.md)
