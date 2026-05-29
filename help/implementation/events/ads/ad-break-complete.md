---
title: 広告ブレーク完了
description: 広告ブレークのすべての広告が終了したことを示します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 9%

---


# 広告ブレーク完了

広告ブレークの完全なイベントシグナルは、広告ブレーク内のすべての広告が終了したことを示します（完了またはスキップします）。 [広告ブレーク開始](ad-break-start.md)までに開いた広告ブレークを閉じます。

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)、[広告ブレーク開始](ad-break-start.md)
* **関連する指標**：なし

>[!IMPORTANT]
>
>すべての`adBreakStart`には一致する`adBreakComplete`が必要です。 クロージングブックエンドを使用しない場合、広告イベントは無視され、広告期間はメインコンテンツに関連付けられます。

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.adBreakComplete"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

`trackEvent`を`AdBreakComplete` イベントタイプで呼び出します。

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

>[!TAB Android]

`trackEvent`を`AdBreakComplete` イベントタイプで呼び出します。

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

>[!TAB Roku]

`sendMediaEvent`を`eventType: "media.adBreakComplete"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

[adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
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

`AdBreakComplete` イベントタイプで`trackEvent`を呼び出します：

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

>[!TAB Chromecast]

`AdBreakComplete` イベントタイプで`trackEvent`を呼び出します：

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete);
```

>[!TAB Media Collection API]

`adBreakComplete`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```

>[!ENDTABS]
