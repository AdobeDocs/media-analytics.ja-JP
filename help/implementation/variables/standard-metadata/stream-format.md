---
title: ストリーム形式
description: ストリーム形式を設定して、品質層（HD、SD、または配信パイプラインで使用するその他のラベル）を特定します。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 13%

---


# ストリーム形式

>[!BEGINSHADEBOX]

*このページでは、**ストリーム形式**変数のデータ収集について説明します。 対応するレポートディメンションについては、[ ストリーム形式](/help/reporting/dimensions/stream-format.md)を参照してください。*

>[!ENDSHADEBOX]

ストリーム形式の変数は、ストリームの品質層を識別します（通常は`"HD"`または`"SD"`ですが、任意の文字列を使用できます）。 配信品質レベルごとに、エンゲージメント、完了率、品質を分割する場合に設定します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.format` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.format` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [ セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内に`streamFormat`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        streamFormat: "HD"
      },
      playhead: 0
    }
  }
});
```

## モバイル SDK

ストリーム形式をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.STREAM_FORMAT`.を使用します。

**iOS （Swift）**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android （Kotlin）**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.STREAM_FORMAT] = "HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku （BrightScript）

`createMediaSession`を使用して`sessionDetails`内に`streamFormat`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "streamFormat": "HD"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails`内の`streamFormat`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "streamFormat": "HD"
        },
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.VideoMetadataKeys.StreamFormat`を使用して、`contextData` オブジェクトにストリーム形式を渡します。

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.StreamFormat] = "HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

## メディアコレクション API

`sessionStart` POST リクエストの`params` オブジェクトに`media.streamFormat`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamFormat": "HD"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
