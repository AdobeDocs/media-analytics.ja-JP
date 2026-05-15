---
title: Ping
description: ハートビートを送信してメディアセッションを維持し、再生の進行状況を定期的に追跡します。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 6%

---


# Ping

ping イベントは、セッションを維持し、再生の進行状況を追跡するハートビートです。 再生中にタイマーに送信します。

* **メインコンテンツ**：再生が開始されてから10秒後にpingが送信され、その後は10秒ごとに送信されます
* **広告コンテンツ**：広告トラッキング中に1秒ごとに

ping リクエスト本文に`params` オブジェクトを含めないでください。

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)
* **関連する指標**：なし

## Web SDK

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

## Mobile SDK

Mobile SDKは、ping イベントを自動的に送信します。 明示的な呼び出しは必要ありません。

## Roku （BrightScript）

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

## Media Edge API

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

## メディア SDK

Media SDKは、ping イベントを自動的に送信します。 明示的な呼び出しは必要ありません。

## メディアコレクション API

タイマー上の[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に`ping`の投稿を送信します。 `params` オブジェクトを含めないでください：

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```
