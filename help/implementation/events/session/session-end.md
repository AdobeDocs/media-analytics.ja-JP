---
title: セッション終了
description: 視聴者がコンテンツを放棄した場合は、直ちにメディアセッションを閉じます。
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 11%

---


# セッション終了

セッション終了イベントは、メディア追跡セッションを直ちに不可逆的に閉じます。 セッション終了はハードクローズです。送信されると、セッションは終了し、それ以降のイベントは追跡できません。 プレーヤーが破壊されたり、ページがアンロードされたりするなど、追加のイベントが続かないことが確実な場合にのみ、セッション終了を使用します。 多くの場合、セッションの有効期限を自然発生的に切り落とすリスクを回避する方が安全です。 視聴者がコンテンツを完了した場合は、代わりに[ セッション完了](session-complete.md)に電話してください。

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
