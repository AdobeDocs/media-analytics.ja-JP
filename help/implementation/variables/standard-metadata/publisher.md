---
title: 発行者
description: オーディオコンテンツパブリッシャーを設定します。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 16%

---


# 発行者

>[!BEGINSHADEBOX]

*このページでは、**Publisher**変数のデータ収集について説明します。 対応するレポートディメンションについては、[発行者](/help/reporting/dimensions/publisher.md)を参照してください。*

>[!ENDSHADEBOX]

パブリッシャー変数は、オーディオコンテンツパブリッシャーの名前（例：ポッドキャストネットワークまたはオーディオブックパブリッシャー）です。 厳選されたオーディオカタログで、メディア企業間のエンゲージメントを比較するために使用できます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.publisher` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.publisher` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [ セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内に`publisher`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        publisher: "Northbridge Audio"
      },
      playhead: 0
    }
  }
});
```

## モバイル SDK

発行者をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.AudioMetadataKeys.PUBLISHER`.を使用します。

**iOS （Swift）**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android （Kotlin）**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku （BrightScript）

`createMediaSession`を使用して`sessionDetails`内に`publisher`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "publisher": "Northbridge Audio"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails`内の`publisher`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "publisher": "Northbridge Audio"
        },
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.AudioMetadataKeys.Publisher`を使用して`contextData` オブジェクト内の発行者を渡します：

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Publisher] = "Northbridge Audio";

tracker.trackSessionStart(mediaInfo, contextData);
```

## メディアコレクション API

`params` オブジェクトに`media.publisher`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.publisher": "Northbridge Audio"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
