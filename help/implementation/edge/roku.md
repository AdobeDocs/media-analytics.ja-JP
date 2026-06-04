---
title: ストリーミングメディア用にRokuを設定する
description: Adobe Experience Platform Roku SDKを設定して、ストリーミングメディアデータをEdge Networkに送信します。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# ストリーミングメディア用にRokuを設定する

[Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku) （BrightScript）は、Roku チャネルのメディアセッションデータを収集し、Edge Networkに送信します。 Rokuはコードで設定されています。タグは使用しません。

* **前提条件**:
   * [Edgeの実装の概要](overview.md)を完了します（[!UICONTROL Media Analytics]が有効になっているスキーマ、データセット、データストリーム）。
   * [GitHub リリース &#x200B;](https://github.com/adobe/aepsdk-roku/releases)からSDKをダウンロードし、[入門ガイド &#x200B;](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md)の説明に従って、チャンネルに追加します。

## AEP Roku SDK メディア版の設定

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
>再生中に、最新の再生ヘッド値を使用して少なくとも1秒に1回、`media.ping` イベントを送信します。 AEP Roku SDKは、これらのpingが正しく機能することに依存しています。

設定キーと完全なAPIについては、[AEP Roku SDK API リファレンス &#x200B;](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md)を参照してください。

## メディアイベントの追跡

セッションが開いたら、各メディアイベントを`sendMediaEvent`で送信します。 正確なペイロードについては、各[&#x200B; イベント &#x200B;](/help/implementation/events/overview.md)および[変数](/help/implementation/variables/overview.md) ページの&#x200B;**Roku** タブを参照してください。

## 次の手順

実装が完了したら、[Edge実装のレポートを設定できます](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform六SDK](https://github.com/adobe/aepsdk-roku)
>* [&#x200B; イベントの概要](/help/implementation/events/overview.md)
>* [変数の概要](/help/implementation/variables/overview.md)
