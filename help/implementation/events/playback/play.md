---
title: Play
description: メディアプレーヤーが再生状態に入ったことを示す信号。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 17%

---


# Play

再生イベントは、メディアプレーヤーが状態を再生に変更したことを示す。 コンテンツの最初の開始時、自動再生時、一時停止またはバッファーの後にプレーヤーが再開されるたびに送信します。 別の再開イベントはありません。[一時停止の開始](pause-start.md)または[&#x200B; バッファーの開始](buffer-start.md)の後の再生イベントが再開として機能します。

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)
* **関連する指標**: [&#x200B; コンテンツ開始](/help/reporting/metrics/content-starts.md)

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.play"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## Mobile SDK

メディアプレーヤーの再生が開始または再開されると、`trackPlay`に電話します。

**iOS （Swift）**

```swift
tracker.trackPlay()
```

**Android （Kotlin）**

```kotlin
tracker.trackPlay()
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.play"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## Media Edge API

[play](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

メディアプレーヤーの再生が開始または再開されたときに`trackPlay`に電話します。

```javascript
tracker.trackPlay();
```

## メディアコレクション API

`play`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```
