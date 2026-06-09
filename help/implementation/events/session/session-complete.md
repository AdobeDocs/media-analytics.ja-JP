---
title: セッション完了
description: 視聴者がメインコンテンツの最後に到達したことを示します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 8%

---


# セッション完了

セッション完了イベントは、視聴者がメインコンテンツの最後に到達したことを示します。 セッションはすぐに閉じません。セッションは、自然に期限切れになるまで開いたままです。 セッションを即座に閉じたい場合は、代わりに[&#x200B; セッション終了](session-end.md)に電話してください。

* **前提条件**: [&#x200B; セッション開始](session-start.md)
* **関連する指標**: [[!UICONTROL &#x200B; コンテンツ完了]](/help/reporting/metrics/content-completes.md)

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

メディアプレーヤーがコンテンツの終わりに達したら、`trackComplete`に電話してください。

```swift
tracker.trackComplete()
```

>[!TAB Android]

メディアプレーヤーがコンテンツの終わりに達したら、`trackComplete`に電話してください。

```kotlin
tracker.trackComplete()
```

>[!TAB Edge六]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

メディアプレーヤーがコンテンツの最後に達したときに`trackComplete`を呼び出します。

```javascript
tracker.trackComplete();
```

>[!TAB Chromecast]

メディアプレーヤーがコンテンツの最後に達したときに`trackComplete`を呼び出します。

```javascript
ADBMobile.media.trackComplete();
```

>[!TAB Roku 2.x]

メディアプレーヤーがコンテンツの最後に達したときに`mediaTrackComplete`を呼び出します。

```brightscript
ADBMobile().mediaTrackComplete()
```

>[!TAB Media Collection API]

`sessionComplete`件の投稿を[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に送信します：

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```

>[!ENDTABS]
