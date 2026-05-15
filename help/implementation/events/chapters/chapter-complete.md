---
title: 章完了
description: チャプターセグメントの再生が終了したことを示します。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 20%

---


# 章完了

チャプターが完了すると、チャプターが再生を終了したことを示すイベントシグナルが表示されます。 ビューアが章の終わりに達したときに送信します。 ビューアが章をスキップした場合は、代わりに[章スキップ &#x200B;](chapter-skip.md)を送信します。

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)、[章開始](chapter-start.md)
* **関連する指標**: [章完了](/help/reporting/metrics/chapter-completes.md)

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.chapterComplete"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## Mobile SDK

`trackEvent`を`ChapterComplete` イベントタイプで呼び出します。

**iOS （Swift）**

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

**Android （Kotlin）**

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.chapterComplete"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterComplete",
        "mediaCollection": {
            "playhead": 240
        }
    }
})
```

## Media Edge API

[chapterComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chaptercomplete) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 240
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

`ChapterComplete` イベントタイプで`trackEvent`を呼び出します：

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

## メディアコレクション API

`chapterComplete`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```
