---
title: Ping
description: ハートビートを送信してメディアセッションを維持し、再生の進行状況を定期的に追跡します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 1%

---


# Ping

ping イベントは、セッションを維持し、再生の進行状況を追跡するハートビートです。 再生中にタイマーに送信します。 Mobile SDKでは、pingは自動的に送信されます。他のすべてのプラットフォームでは、指定した間隔で手動で送信する必要があります。

* **メインコンテンツ**：再生が開始されてから10秒後にpingが送信され、その後は10秒ごとに送信されます
* **広告コンテンツ**：広告トラッキング中に1秒ごとに

ping リクエスト本文に`params` オブジェクトを含めないでください。

* **前提条件**: [ セッション開始](../session/session-start.md)
* **関連する指標**：なし

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

`eventType: "media.ping"`様との定期的な`sendEvent`通話をスケジュールします。 各呼び出しの現在の再生位置に`playhead`を更新します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.ping",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 10
    }
  }
});
```

>[!TAB iOS]

Mobile SDKは、ping イベントを自動的に送信します。 明示的な呼び出しは必要ありません。

>[!TAB Android]

Mobile SDKは、ping イベントを自動的に送信します。 明示的な呼び出しは必要ありません。

>[!TAB Edge六]

`eventType: "media.ping"`様との定期的な`sendMediaEvent`通話をスケジュールします。 各呼び出しの現在の再生位置に`playhead`を更新します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.ping",
        "mediaCollection": {
            "playhead": 10
        }
    }
})
```

>[!TAB Media Edge API]

タイマーで[ping](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ping/) エンドポイントを呼び出します。 Adobeでは、メイン再生開始後10秒、その後10秒ごと、および広告トラッキング中の1秒ごとに最初のpingを実行することをお勧めします。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/ping?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.ping",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 10
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Media SDKは、ping イベントを自動的に送信します。 明示的な呼び出しは必要ありません。

>[!TAB Chromecast]

Chromecast SDKは、ping イベントを自動的に送信します。 明示的な呼び出しは必要ありません。

>[!TAB Roku 2.x]

Media SDKは、イベントループで`processMediaMessages`を呼び出す限り、ping イベントを自動的に送信します。 再生ヘッドを更新して、各pingが現在の位置をレポートするようにします。

```brightscript
ADBMobile().mediaUpdatePlayhead(10)
```

>[!TAB Media Collection API]

タイマー上の[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に`ping`の投稿を送信します。 `params` オブジェクトを含めないでください：

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```

>[!ENDTABS]
