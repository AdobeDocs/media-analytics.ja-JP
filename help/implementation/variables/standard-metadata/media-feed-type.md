---
title: メディアフィードタイプ
description: 地域や品質によって異なるコンテンツのブロードキャストフィードのタイプ（East-HDやWest-SDなど）を特定します。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 13%

---


# メディアフィードタイプ

>[!BEGINSHADEBOX]

*このページでは、**メディアフィードの種類**変数のデータ収集について説明します。 対応するレポートディメンションについては、[ メディアフィードの種類](/help/reporting/dimensions/media-feed-type.md)を参照してください。*

>[!ENDSHADEBOX]

メディアフィードのタイプ変数は、ブロードキャストフィードを識別します（例：`"East-HD"`、`"West-SD"`、または`"4K"`）。 複数の地域または品質のフィードを通じて同じコンテンツが配信され、フィードごとにエンゲージメントを分割する必要がある場合に使用します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.feed` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.feed` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [ セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内に`feed`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        feed: "East-HD"
      },
      playhead: 0
    }
  }
});
```

## モバイル SDK

フィードの種類をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.MEDIA_FEED`.を使用します。

**iOS （Swift）**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android （Kotlin）**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku （BrightScript）

`createMediaSession`を使用して`sessionDetails`内に`feed`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "feed": "East-HD"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails`内の`feed`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "feed": "East-HD"
        },
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.VideoMetadataKeys.Feed`を使用して`contextData` オブジェクトにフィードを渡します：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Feed] = "East-HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

## メディアコレクション API

`params` オブジェクトに`media.feed`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.feed": "East-HD"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
