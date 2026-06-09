---
title: エラー
description: メディアプレーヤーでエラーが発生したことを示します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 9%

---


# エラー

エラーイベントは、メディアプレーヤーでエラーが発生したことを示します。 エラーを追跡しても、セッションは閉じません。 エラーにより再生が続行されない場合は、エラーイベントの後に[&#x200B; セッション終了](session/session-end.md)を呼び出します。

* **前提条件**: [&#x200B; セッション開始](session/session-start.md)
* **関連する指標**: [[!UICONTROL 影響を受けるストリーム &#x200B;]](/help/reporting/metrics/error-impacted-streams.md)

`errorDetails.source` プロパティで使用できる値は、2つだけです。`player` （メディアプレーヤーで発生したエラー）と`external` （CDNやネットワークなどの外部ソースからのエラー）。

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

エラーID文字列で`trackError`を呼び出します。

```swift
tracker.trackError(errorId: "media-error-001")
```

>[!TAB Android]

エラーID文字列で`trackError`を呼び出します。

```kotlin
tracker.trackError("media-error-001")
```

>[!TAB Edge六]

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

>[!TAB Media Edge API]

必要な`errorDetails`を使用して[&#x200B; エラー](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/) エンドポイントを呼び出します。

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

エラーID文字列で`trackError`を呼び出します：

```javascript
tracker.trackError("media-error-001");
```

>[!TAB Chromecast]

エラーID文字列で`trackError`を呼び出します：

```javascript
ADBMobile.media.trackError("media-error-001");
```

>[!TAB Roku 2.x]

エラーIDとエラーソースを指定して`mediaTrackError`を呼び出します。 プレーヤーのエラーに`ERROR_SOURCE_PLAYER`定数を使用します。

```brightscript
adb = ADBMobile()
adb.mediaTrackError("media-error-001", adb.ERROR_SOURCE_PLAYER)
```

>[!TAB Media Collection API]

`error`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

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

>[!ENDTABS]
