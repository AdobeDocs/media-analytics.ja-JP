---
title: ストリーミングメディア用のMedia Edge APIの設定
description: Media Edge APIを使用して、ストリーミングメディアデータをEdge Networkに直接送信します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# ストリーミングメディア用のMedia Edge APIの設定

Web SDK、モバイルSDK、Roku Edge SDKを使用できない場合（カスタムランタイムやサポートされていないランタイムなど）、Media Edge APIを使用して、ストリーミングメディアデータをEdge Networkに直接送信できます。 APIはRESTful HTTP呼び出しを使用し、完全にカスタマイズ可能です。

* **前提条件**: [Edgeの実装の概要](overview.md) （スキーマ、データセット、データストリーム、および[!UICONTROL Media Analytics]が有効）を完了します。

## Edge Networkへのメディアイベントの送信

メディアイベントは`/ee/va/v1/` エンドポイントに送信され、`configId` クエリパラメーターによってデータストリームにキーが設定されます。 例えば、セッションは`sessionStart`へのPOSTで始まります。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId=<datastreamID>" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": { "name": "video-123", "playerName": "player_name", "contentType": "vod", "length": 128, "channel": "sample_channel" },
        "playhead": 0
      }
    }
  }]
}'
```

応答は、後続のすべてのイベントに含める必要があるセッション IDを返します。 完全なエンドポイントセット、リクエスト/レスポンス形式、およびOpenAPI仕様については、[Media Edge API リファレンス &#x200B;](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)を参照してください。

## メディアイベントの追跡

正確なペイロードについては、各[&#x200B; イベント &#x200B;](/help/implementation/events/overview.md)および[変数](/help/implementation/variables/overview.md) ページの「**Media Edge API**」タブを参照してください。

## 次の手順

実装が完了したら、[Edge実装のレポートを設定できます](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Media Edge API リファレンス &#x200B;](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)
>* [&#x200B; イベントの概要](/help/implementation/events/overview.md)
>* [変数の概要](/help/implementation/variables/overview.md)
