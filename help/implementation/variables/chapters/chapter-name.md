---
title: 章名
description: 各章のわかりやすい名前を設定して、章レベルのレポートを章タイトルで分割できるようにします。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 13%

---


# 章名

>[!BEGINSHADEBOX]

*このページでは、**章名**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[章名](/help/reporting/dimensions/chapter-name.md)を参照してください。*

>[!ENDSHADEBOX]

章名変数は、人間が読み取れる章のタイトルです（例：`"Pilot Episode - Opening"`）。 コンテンツがチャプターに分割されている`media.chapterStart` イベントごとに設定します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.chapter.friendlyName` |
| **XDM コレクションフィールド** | [`mediaCollection.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.chapter.friendlyName` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [章の開始](/help/implementation/events/chapters/chapter-start.md)、章の終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.chapterDetails`内に`friendlyName`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Pilot Episode - Opening",
        index: 1,
        offset: 0,
        length: 240
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## モバイル SDK

章名を最初の（`name`）引数として`createChapterObject`に渡します。

**iOS （Swift）**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android （Kotlin）**

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku （BrightScript）

`media.chapterStart`の`sendMediaEvent`を呼び出す場合、`mediaCollection.chapterDetails`内に`friendlyName`を設定します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Pilot Episode - Opening",
                "index": 1,
                "offset": 0,
                "length": 240
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.chapterDetails`内の`friendlyName`で[chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) エンドポイントを呼び出します。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "friendlyName": "Pilot Episode - Opening",
          "index": 1,
          "offset": 0,
          "length": 240
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

章名を最初の引数として`ADB.Media.createChapterObject`に渡します。

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## メディアコレクション API

`chapterStart` POST リクエストの`params` オブジェクトに`media.chapter.friendlyName`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
