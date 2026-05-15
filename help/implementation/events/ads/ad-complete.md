---
title: 広告が完了
description: 個々の広告が再生を終了したことを示します。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 15%

---


# 広告が完了

広告完了イベントは、個々の広告が再生を完了したことを示します。 広告の再生後から完了まで送信します。 視聴者が広告をスキップした場合は、代わりに[広告スキップ ](ad-skip.md)を送信します。

* **前提条件**: [ セッション開始](../session/session-start.md)、[ アドブレーク開始](ad-break-start.md)、[ アドスタート ](ad-start.md)
* **関連する指標**: [広告が](/help/reporting/metrics/ad-completes.md)を完了しました

>[!IMPORTANT]
>
>1つの広告が再生される場合でも、このイベントは`adBreakStart`と`adBreakComplete`個のブックエンドで囲む必要があります。 これらのブックエンドがないと、広告イベントは無視され、広告期間はメインコンテンツ期間としてカウントされます。

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.adComplete"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

## Mobile SDK

`trackEvent`を`AdComplete` イベントタイプで呼び出します。

**iOS （Swift）**

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

**Android （Kotlin）**

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.adComplete"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

## Media Edge API

[adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

`AdComplete` イベントタイプで`trackEvent`を呼び出します：

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

## メディアコレクション API

`adComplete`件の投稿を[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```
