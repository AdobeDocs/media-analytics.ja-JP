---
title: 日パート
description: コンテンツがブロードキャストまたは再生されたときの時間帯バケット（午前、午後、時間、深夜）を設定します。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 13%

---


# 日パート

>[!BEGINSHADEBOX]

*このページでは、**日パート**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[日パート &#x200B;](/help/reporting/dimensions/day-part.md)を参照してください。*

>[!ENDSHADEBOX]

日別パート変数は、コンテンツがブロードキャストまたは再生された時間帯バケットです（例：`"Morning"`、`"Afternoon"`、`"Primetime"`、または`"Late Night"`）。 任意の文字列を使用できます。 視聴者のローカルタイムゾーンに依存せずに、時間帯全体のエンゲージメントを比較するために使用します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.dayPart` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | セッション開始、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内に`dayPart`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        dayPart: "Primetime"
      },
      playhead: 0
    }
  }
});
```

## モバイル SDK

日付部分をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.DAY_PART`.を使用します。

**iOS （Swift）**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android （Kotlin）**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku （BrightScript）

`createMediaSession`を使用して`sessionDetails`内に`dayPart`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "dayPart": "Primetime"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails`内の`dayPart`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "dayPart": "Primetime"
        },
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.VideoMetadataKeys.DayPart`を使用して、`contextData` オブジェクトの日付部分を渡します：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.DayPart] = "Primetime";

tracker.trackSessionStart(mediaInfo, contextData);
```

## メディアコレクション API

`params` オブジェクトに`media.dayPart`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.dayPart": "Primetime"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
