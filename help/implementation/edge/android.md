---
title: ストリーミングメディア用にAndroidを設定する
description: Android上のAdobe Experience Platform Mobile SDKを設定して、ストリーミングメディアデータをEdge Networkに送信します。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# ストリーミングメディア用にAndroidを設定する

Adobe Streaming Media for Edge Network拡張機能（`EdgeMedia`）は、Android アプリでメディアセッションデータを収集し、それをEdge Networkに送信します。 このページでは、コード内の設定について説明します。 代わりにTags モバイルプロパティを使用してSDKを設定するには、「[ タグを使用したストリーミングメディア用にAndroidを設定する](android-tags.md)」を参照してください。

* **前提条件**:
   * [Edgeの実装の概要](overview.md)を完了します（[!UICONTROL Media Analytics]が有効になっているスキーマ、データセット、データストリーム）。
   * アプリに`Core`、`Edge`、`EdgeIdentity`および`EdgeMedia`拡張機能を追加します。 インストールと登録については、[Edge Network用Adobe Streaming Media](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)を参照してください。

## Android用メディアの設定

SDKを初期化する際に、メディア設定キーを設定します。

```kotlin
val configuration = mapOf(
  "edgeMedia.channel" to "sample_channel",
  "edgeMedia.playerName" to "player_name",
  "edgeMedia.appVersion" to "app_version"
)
MobileCore.updateConfiguration(configuration)
```

次に、メディアセッションを管理するためのトラッカーを作成します。

```kotlin
val tracker = Media.createTracker()
```

コンフィギュレーションキーと完全なトラッカーAPIについては、[Media for Edge Network API リファレンス ](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/)を参照してください。

## メディアイベントの追跡

トラッカーを作成したら、トラッカーのメソッドを使用して各メディアイベントを追跡します。 正確な呼び出しについては、各[event](/help/implementation/events/overview.md)および[variable](/help/implementation/variables/overview.md) ページの「**Android**」タブを参照してください。

## 次の手順

実装が完了したら、[Edge実装のレポートを設定できます](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Edge Network用Adobe Streaming Media](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [ タグ付きストリーミングメディア用にAndroidを設定](android-tags.md)
>* [ イベントの概要](/help/implementation/events/overview.md)
