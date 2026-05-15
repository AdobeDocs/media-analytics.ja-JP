---
title: セッション終了
description: 視聴者がコンテンツを放棄した場合は、直ちにメディアセッションを閉じます。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 14%

---


# セッション終了

セッション終了イベントは、メディアトラッキングセッションを直ちに閉じます。 ビューアが最後に到達する前にコンテンツを放棄し、同じセッションで後続のイベントを追跡しない場合に使用します。 視聴者がコンテンツを完了した場合は、代わりに[ セッション完了](session-complete.md)に電話してください。

明示的なセッション終了がなければ、イベントなしの10分または再生ヘッドなしの30分が経過すると、セッションは自動的に終了します。

* **前提条件**: [ セッション開始](session-start.md)
* **関連する指標**：なし

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.sessionEnd"`と呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

ビューアーがプレーヤーを閉じるか、離れるときに`trackSessionEnd`に電話します。

**iOS （Swift）**

```swift
tracker.trackSessionEnd()
```

**Android （Kotlin）**

```kotlin
tracker.trackSessionEnd()
```

## Roku （BrightScript）

`sendMediaEvent`を`eventType: "media.sessionEnd"`と呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## Media Edge API

[sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

ビューアーがプレーヤーを閉じるか、離れるときに`trackSessionEnd`に電話します。

```javascript
tracker.trackSessionEnd();
```

## メディアコレクション API

`sessionEnd`件の投稿を[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```
