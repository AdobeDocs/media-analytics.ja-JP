---
title: 広告が完了
description: 個々の広告が再生を終了したことを示します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 9%

---


# 広告が完了

広告完了イベントは、個々の広告が再生を完了したことを示します。 広告の再生後から完了まで送信します。 視聴者が広告をスキップした場合は、代わりに[広告スキップ ](ad-skip.md)を送信します。

* **前提条件**: [ セッション開始](../session/session-start.md)、[ アドブレーク開始](ad-break-start.md)、[ アドスタート ](ad-start.md)
* **関連する指標**: [[!UICONTROL 広告が]](/help/reporting/metrics/ad-completes.md)を完了しました

>[!IMPORTANT]
>
>1つの広告が再生される場合でも、このイベントは`adBreakStart`と`adBreakComplete`個のブックエンドで囲む必要があります。 これらのブックエンドがないと、広告イベントは無視され、広告期間はメインコンテンツ期間としてカウントされます。

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

`trackEvent`を`AdComplete` イベントタイプで呼び出します。

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

>[!TAB Android]

`trackEvent`を`AdComplete` イベントタイプで呼び出します。

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

>[!TAB Roku]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`AdComplete` イベントタイプで`trackEvent`を呼び出します：

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

>[!TAB Chromecast]

`AdComplete` イベントタイプで`trackEvent`を呼び出します：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
```

>[!TAB Media Collection API]

`adComplete`件の投稿を[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```

>[!ENDTABS]
