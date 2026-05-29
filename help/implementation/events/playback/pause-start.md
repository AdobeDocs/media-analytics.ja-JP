---
title: 一時停止して開始
description: ユーザーがメディア再生を一時停止したことを示します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 10%

---


# 一時停止して開始

一時停止の開始イベントは、ユーザーが再生を一時停止したことを示します。 別の再開イベントはありません。再生の再開時に[Play](play.md) イベントを送信します。

* **前提条件**: [ セッション開始](../session/session-start.md)
* **関連する指標**: [[!UICONTROL  イベントを一時停止]](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>再開イベントタイプがありません。 `pauseStart`の後に[`play`](play.md) イベントを送信すると、再開が推測されます。

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

ユーザーが再生を一時停止したときに`trackPause`を呼び出します。

```swift
tracker.trackPause()
```

>[!TAB Android]

ユーザーが再生を一時停止したときに`trackPause`を呼び出します。

```kotlin
tracker.trackPause()
```

>[!TAB Roku]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

ユーザーが再生を一時停止したときに`trackPause`を呼び出します。

```javascript
tracker.trackPause();
```

>[!TAB Chromecast]

ユーザーが再生を一時停止したときに`trackPause`を呼び出します。

```javascript
ADBMobile.media.trackPause();
```

>[!TAB Media Collection API]

`pauseStart`件の投稿を[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```

>[!ENDTABS]
