---
title: ストリーミングメディア用のMedia Edge APIの設定
description: Media Edge APIを使用して、ストリーミングメディアデータをEdge Networkに直接送信します。
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
