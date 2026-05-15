---
title: エラー
description: メディアプレーヤーでエラーが発生したことを示します。
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 16%

---


# エラー

エラーイベントは、メディアプレーヤーでエラーが発生したことを示します。 エラーを追跡しても、セッションは閉じません。 エラーにより再生が続行されない場合は、エラーイベントの後に[ セッション終了](session/session-end.md)を呼び出します。

* **前提条件**: [ セッション開始](session/session-start.md)
* **関連する指標**: [影響を受けるストリーム ](/help/reporting/metrics/error-impacted-streams.md)

`errorDetails.source` プロパティで使用できる値は、2つだけです。`player` （メディアプレーヤーで発生したエラー）と`external` （CDNやネットワークなどの外部ソースからのエラー）。

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)に`eventType: "media.error"`と必須`errorDetails`を呼び出します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## Mobile SDK

エラーID文字列で`trackError`を呼び出します。

**iOS （Swift）**

```swift
tracker.trackError(errorId: "media-error-001")
```

**Android （Kotlin）**

```kotlin
tracker.trackError("media-error-001")
```

## Roku （BrightScript）

`sendMediaEvent`に`eventType: "media.error"`と必須`errorDetails`を呼び出します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

## Media Edge API

必要な`errorDetails`を使用して[ エラー](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## メディア SDK

エラーID文字列で`trackError`を呼び出します：

```javascript
tracker.trackError("media-error-001");
```

## メディアコレクション API

`error`件の投稿を[ イベントエンドポイント ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```
