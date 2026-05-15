---
title: 作成者
description: コンテンツのクリエイターまたは制作スタジオを設定します。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 16%

---


# 作成者

>[!BEGINSHADEBOX]

*このページでは、**Originator**変数のデータ収集について説明します。 対応するレポートディメンションについては、[発信元](/help/reporting/dimensions/originator.md)を参照してください。*

>[!ENDSHADEBOX]

元の変数は、コンテンツの作成者または実稼動スタジオです（例：`"Warner Brothers"`、`"Sony"`、または`"Disney"`）。 コンテンツ所有者や権利者のエンゲージメントを比較するために利用できます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.originator` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.originator`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.originator` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [ セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内に`originator`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        originator: "Warner Brothers"
      },
      playhead: 0
    }
  }
});
```

## モバイル SDK

発信元をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.ORIGINATOR`.を使用します。

**iOS （Swift）**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android （Kotlin）**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ORIGINATOR] = "Warner Brothers"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku （BrightScript）

`createMediaSession`を使用して`sessionDetails`内に`originator`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "originator": "Warner Brothers"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails`内の`originator`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "originator": "Warner Brothers"
        },
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.VideoMetadataKeys.Originator`を使用して、`contextData` オブジェクトの発信元を渡します：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Originator] = "Warner Brothers";

tracker.trackSessionStart(mediaInfo, contextData);
```

## メディアコレクション API

`params` オブジェクトに`media.originator`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.originator": "Warner Brothers"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
