---
title: 広告スキップ
description: 視聴者が広告をスキップしたことを知らせるシグナル。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

---


# 広告スキップ

広告スキップイベントは、視聴者が広告を終了する前にスキップしたことを示します。 ビューアがスキップボタンを選択したときに送信します。 広告が完了まで再生される場合は、代わりに[Ad complete](ad-complete.md)を送信します。

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)、[&#x200B; アドブレーク開始](ad-break-start.md)、[&#x200B; アドスタート &#x200B;](ad-start.md)
* **関連する指標**：なし

>[!IMPORTANT]
>
>1つの広告が再生される場合でも、このイベントは`adBreakStart`と`adBreakComplete`個のブックエンドで囲む必要があります。 これらのブックエンドがないと、広告イベントは無視され、広告期間はメインコンテンツ期間としてカウントされます。

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.adSkip"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 5
    }
  }
});
```

## Mobile SDK

`trackEvent`を`AdSkip` イベントタイプで呼び出します。

**iOS （Swift）**

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

**Android （Kotlin）**

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.adSkip"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adSkip",
        "mediaCollection": {
            "playhead": 5
        }
    }
})
```

## Media Edge API

[adSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adskip) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 5
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

`AdSkip` イベントタイプで`trackEvent`を呼び出します：

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

## メディアコレクション API

`adSkip`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```
