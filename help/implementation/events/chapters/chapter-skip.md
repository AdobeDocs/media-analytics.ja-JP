---
title: 章のスキップ
description: 視聴者が章をスキップしたことを知らせる。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 18%

---


# 章のスキップ

章スキップイベントは、ビューアが章を終了する前にスキップしたことを示します。 ビューアが章の境界を通過したときに、完了まで見ずに送信します。 章が最後まで再生される場合は、[章完了](chapter-complete.md)を送信します。

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)、[章開始](chapter-start.md)
* **関連する指標**：なし

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.chapterSkip"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

## Mobile SDK

`trackEvent`を`ChapterSkip` イベントタイプで呼び出します。

**iOS （Swift）**

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

**Android （Kotlin）**

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.chapterSkip"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterSkip",
        "mediaCollection": {
            "playhead": 60
        }
    }
})
```

## Media Edge API

[chapterSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterskip) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

`ChapterSkip` イベントタイプで`trackEvent`を呼び出します：

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

## メディアコレクション API

`chapterSkip`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```
