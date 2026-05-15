---
title: 一時停止して開始
description: ユーザーがメディア再生を一時停止したことを示します。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 19%

---


# 一時停止して開始

一時停止の開始イベントは、ユーザーが再生を一時停止したことを示します。 別の再開イベントはありません。再生の再開時に[Play](play.md) イベントを送信します。

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)
* **関連する指標**: [&#x200B; イベントを一時停止](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>再開イベントタイプがありません。 `pauseStart`の後に[`play`](play.md) イベントを送信すると、再開が推測されます。

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.pauseStart"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

## Mobile SDK

ユーザーが再生を一時停止したときに`trackPause`を呼び出します。

**iOS （Swift）**

```swift
tracker.trackPause()
```

**Android （Kotlin）**

```kotlin
tracker.trackPause()
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.pauseStart"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

## Media Edge API

[pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

ユーザーが再生を一時停止したときに`trackPause`を呼び出します。

```javascript
tracker.trackPause();
```

## メディアコレクション API

`pauseStart`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```
