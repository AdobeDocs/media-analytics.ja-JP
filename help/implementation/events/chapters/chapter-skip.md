---
title: 章のスキップ
description: 視聴者が章をスキップしたことを知らせる。
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
source-wordcount: '157'
ht-degree: 9%
---

# 章のスキップ

章スキップイベントは、ビューアが章を終了する前にスキップしたことを示します。 ビューアが章の境界を通過したときに、完了まで見ずに送信します。 章が最後まで再生される場合は、[章完了](chapter-complete.md)を送信します。

* **前提条件**: [ セッション開始](../session/session-start.md)、[章開始](chapter-start.md)
* **関連する指標**：なし

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

`trackEvent`を`ChapterSkip` イベントタイプで呼び出します。

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

>[!TAB Android]

`trackEvent`を`ChapterSkip` イベントタイプで呼び出します。

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

>[!TAB Edge六]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`ChapterSkip` イベントタイプで`trackEvent`を呼び出します：

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

>[!TAB Chromecast]

`ChapterSkip` イベントタイプで`trackEvent`を呼び出します：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
```

>[!TAB Roku 2.x]

`MEDIA_CHAPTER_SKIP` イベントタイプで`mediaTrackEvent`を呼び出します：

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_CHAPTER_SKIP)
```

>[!TAB Media Collection API]

`chapterSkip`件の投稿を[ イベントエンドポイント ](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events)に送信します：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```

>[!ENDTABS]
