---
title: ビットレートの変更
description: 再生ビットレートが変更されたことを示します。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 14%

---


# ビットレートの変更

ビットレート変更イベントは、プレーヤーが新しい再生ビットレートを交渉したことを示します。 再生中にビットレートが変更されるたびに送信します。 新しいビットレート値をQoE データに含めて、バックエンドが[平均ビットレート ](/help/reporting/metrics/average-bitrate.md)とビットレートごとのバケット ディメンションを計算できるようにします。

* **前提条件**: [ セッション開始](../session/session-start.md)
* **関連する指標**: [ ビットレートの変更](/help/reporting/metrics/bitrate-changes.md)

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.bitrateChange"`で呼び出し、新しいビットレートを`qoeDataDetails`で呼び出します。

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## Mobile SDK

新しいビットレートでQoE オブジェクトを作成し、ビットレート変更イベントが発生する前にトラッカーを更新します。

**iOS （Swift）**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android （Kotlin）**

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.bitrateChange"`で呼び出し、新しいビットレートを`qoeDataDetails`で呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

`qoeDataDetails`の新しいビットレートで[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bitrateChange?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

新しいビットレートでQoE オブジェクトを作成し、トラッカーを更新します。

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## メディアコレクション API

`qoeData`の新しいビットレートを使用して、[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に`bitrateChange` POSTを送信します。

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "qoeData": {
    "media.qoe.bitrate": 3200
  }
}
```
