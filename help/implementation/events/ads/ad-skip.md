---
title: 広告スキップ
description: 視聴者が広告をスキップしたことを知らせるシグナル。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---


# 広告スキップ

広告スキップイベントは、視聴者が広告を終了する前にスキップしたことを示します。 ビューアがスキップボタンを選択したときに送信します。 広告が完了まで再生される場合は、代わりに[Ad complete](ad-complete.md)を送信します。

* **前提条件**: [ セッション開始](../session/session-start.md)、[ アドブレーク開始](ad-break-start.md)、[ アドスタート ](ad-start.md)
* **関連する指標**：なし

>[!IMPORTANT]
>
>1つの広告が再生される場合でも、このイベントは`adBreakStart`と`adBreakComplete`個のブックエンドで囲む必要があります。 これらのブックエンドがないと、広告イベントは無視され、広告期間はメインコンテンツ期間としてカウントされます。

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

`trackEvent`を`AdSkip` イベントタイプで呼び出します。

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

>[!TAB Android]

`trackEvent`を`AdSkip` イベントタイプで呼び出します。

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

>[!TAB Edge六]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`AdSkip` イベントタイプで`trackEvent`を呼び出します：

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

>[!TAB Chromecast]

`AdSkip` イベントタイプで`trackEvent`を呼び出します：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdSkip);
```

>[!TAB Roku 2.x]

`MEDIA_AD_SKIP` イベントタイプで`mediaTrackEvent`を呼び出します：

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_SKIP)
```

>[!TAB Media Collection API]

`adSkip`件の投稿を[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```

>[!ENDTABS]
