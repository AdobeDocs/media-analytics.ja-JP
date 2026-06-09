---
title: Play
description: メディアプレーヤーが再生状態に入ったことを示す信号。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 9%

---


# Play

再生イベントは、メディアプレーヤーが状態を再生に変更したことを示す。 コンテンツの最初の開始時、自動再生時、一時停止またはバッファーの後にプレーヤーが再開されるたびに送信します。 別の再開イベントはありません。[一時停止の開始](pause-start.md)または[&#x200B; バッファーの開始](buffer-start.md)の後の再生イベントが再開として機能します。

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)
* **関連する指標**: [[!UICONTROL &#x200B; コンテンツ開始]](/help/reporting/metrics/content-starts.md)

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.play"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

メディアプレーヤーの再生が開始または再開されると、`trackPlay`に電話します。

```swift
tracker.trackPlay()
```

>[!TAB Android]

メディアプレーヤーの再生が開始または再開されると、`trackPlay`に電話します。

```kotlin
tracker.trackPlay()
```

>[!TAB Edge六]

`sendMediaEvent`を`eventType: "media.play"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

[play](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
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

メディアプレーヤーの再生が開始または再開されたときに`trackPlay`に電話します。

```javascript
tracker.trackPlay();
```

>[!TAB Chromecast]

メディアプレーヤーの再生が開始または再開されたときに`trackPlay`に電話します。

```javascript
ADBMobile.media.trackPlay();
```

>[!TAB Roku 2.x]

メディアプレーヤーの再生が開始または再開されたときに`mediaTrackPlay`に電話します。

```brightscript
ADBMobile().mediaTrackPlay()
```

>[!TAB Media Collection API]

`play`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```

>[!ENDTABS]
