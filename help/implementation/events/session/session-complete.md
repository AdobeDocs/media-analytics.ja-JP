---
title: セッション完了
description: 視聴者がメインコンテンツの最後に到達したことを示します。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 16%

---


# セッション完了

セッション完了イベントは、視聴者がメインコンテンツの最後に到達したことを示します。 セッションはすぐに閉じません。セッションは、自然に期限切れになるまで開いたままです。 セッションを即座に閉じたい場合は、代わりに[ セッション終了](session-end.md)に電話してください。

* **前提条件**: [ セッション開始](session-start.md)
* **関連する指標**: [ コンテンツ完了](/help/reporting/metrics/content-completes.md)

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.sessionComplete"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

## Mobile SDK

メディアプレーヤーがコンテンツの終わりに達したら、`trackComplete`に電話してください。

**iOS （Swift）**

```swift
tracker.trackComplete()
```

**Android （Kotlin）**

```kotlin
tracker.trackComplete()
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.sessionComplete"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

## Media Edge API

[sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

メディアプレーヤーがコンテンツの最後に達したときに`trackComplete`を呼び出します。

```javascript
tracker.trackComplete();
```

## メディアコレクション API

`sessionComplete`件の投稿を[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```
