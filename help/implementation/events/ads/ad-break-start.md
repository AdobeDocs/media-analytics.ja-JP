---
title: 広告休憩の開始
description: 広告ブレークの開始（1つ以上の広告のシーケンス）を通知します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 7%

---


# 広告休憩の開始

広告枠の開始イベントは、広告枠の開始を示します。 広告ブレークとは、1つ以上の広告のシーケンスです。 1つの広告が再生される場合でも、`adStart`、`adComplete`および`adSkip` イベントごとに`adBreakStart`と`adBreakComplete` ペアの間で発生する必要があります。

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)
* **関連する指標**：なし

>[!IMPORTANT]
>
>広告イベント （`adStart`、`adComplete`、`adSkip`）は、`adBreakStart`および`adBreakComplete`件のブックエンドなしで無視されます。 指標を使用しない場合、広告期間はメインコンテンツ期間に起因し、集約レポートデータに影響します。

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)に`eventType: "media.adBreakStart"`と必須`advertisingPodDetails`を呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

広告ブレーク名、位置、開始時間を`createAdBreakObject`に渡してから、`trackEvent`に電話してください。

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

広告ブレーク名、位置、開始時間を`createAdBreakObject`に渡してから、`trackEvent`に電話してください。

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1,
                                              0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku]

`sendMediaEvent`に`eventType: "media.adBreakStart"`と必須`advertisingPodDetails`を呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

必要な`advertisingPodDetails`で[adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingPodDetails": {
          "index": 0,
          "offset": 0
        }
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

広告ブレーク名、位置、開始時間を`ADB.Media.createAdBreakObject`に渡します：

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

広告ブレーク名、位置、開始時間を`ADBMobile.media.createAdBreakObject`に渡します：

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",  // name
  1,           // position
  0            // start time (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Media Collection API]

`adBreakStart`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll",
    "media.ad.podIndex": 1,
    "media.ad.podSecond": 0
  }
}
```

>[!ENDTABS]
