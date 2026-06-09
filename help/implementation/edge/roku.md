---
title: ストリーミングメディア用にRoku Edgeを設定する
description: Adobe Experience Platform Roku SDKを設定して、ストリーミングメディアデータをEdge Networkに送信します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# ストリーミングメディア用にRoku Edgeを設定する

[Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku) （BrightScript）は、Roku チャネルのメディアセッションデータを収集し、Edge Networkに送信します。 Rokuはコードで設定されています。タグは使用しません。

* **前提条件**:
   * [Edgeの実装の概要](overview.md)を完了します（[!UICONTROL Media Analytics]が有効になっているスキーマ、データセット、データストリーム）。
   * [GitHub リリース ](https://github.com/adobe/aepsdk-roku/releases)からSDKをダウンロードし、[入門ガイド ](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md)の説明に従って、チャンネルに追加します。

## Roku Edge SDK for mediaの設定

SDKを初期化し、データストリームとメディアの設定を行います。

```brightscript
m.aepSdk = AdobeAEPSDKInit()
ADB_CONSTANTS = AdobeAEPSDKConstants()

configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<datastreamID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "sample_channel"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
m.aepSdk.updateConfiguration(configuration)
```

次に、`createMediaSession`とのセッションを開きます：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": { "name": "video-123", "length": 128, "contentType": "vod", "streamType": "video" },
            "playhead": 0
        }
    }
})
```

>[!IMPORTANT]
>
>再生中に、最新の再生ヘッド値を使用して少なくとも1秒に1回、`media.ping` イベントを送信します。 Roku Edge SDKは、これらのpingが正しく機能することに依存しています。

設定キーと完全なAPIについては、[Roku Edge SDK API リファレンス ](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md)を参照してください。

## メディアイベントの追跡

セッションが開いたら、各メディアイベントを`sendMediaEvent`で送信します。 正確なペイロードについては、各[event](/help/implementation/events/overview.md)および[variable](/help/implementation/variables/overview.md) ページの&#x200B;**Roku Edge** タブを参照してください。

## 次の手順

実装が完了したら、[Edge実装のレポートを設定できます](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform六SDK](https://github.com/adobe/aepsdk-roku)
>* [ イベントの概要](/help/implementation/events/overview.md)
>* [変数の概要](/help/implementation/variables/overview.md)
