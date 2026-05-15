---
title: バッファー開始
description: メディアプレーヤーがバッファリング状態になったことを示す信号。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 15%

---


# バッファー開始

バッファー開始イベントは、メディアプレーヤーがバッファリング状態に入ったことを示します。

* **前提条件**: [ セッション開始](../session/session-start.md)
* **関連する指標**: [ バッファーイベント ](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**XDM ベースのAPI （Web SDK、Roku、Media Edge API、Media Collection API）:** バッファー再開イベントの種類はありません。`bufferStart`の後に[`play`](play.md) イベントを送信すると、バッファーの終了が推測されます。
>
>**モバイル SDK:** バッファリングを終了したら`trackEvent(BufferComplete)`に電話し、`trackPlay()`に電話して再生を再開します。

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.bufferStart"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bufferStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

プレーヤーがバッファリング状態に入ったときに`BufferStart`で`trackEvent`に電話し、終了したときに`BufferComplete`に電話します。

**iOS （Swift）**

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

**Android （Kotlin）**

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.bufferStart"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## Media Edge API

[bufferStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bufferstart/) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bufferStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bufferStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

`BufferStart` イベントタイプで`trackEvent`を呼び出します：

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

## メディアコレクション API

`bufferStart`件の投稿を[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```
