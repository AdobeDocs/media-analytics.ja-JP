---
title: チャプターオフセット
description: コンテンツ内のチャプターのオフセットを、開始から秒単位で設定します。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 12%

---


# チャプターオフセット

>[!BEGINSHADEBOX]

*このページでは、**章オフセット**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[章オフセット &#x200B;](/help/reporting/dimensions/chapter-offset.md)を参照してください。*

>[!ENDSHADEBOX]

チャプターオフセット変数は、コンテンツ内のチャプターのオフセットです。先頭から秒単位で測定されます。 最初のチャプターは通常`0`をオフセットしています。後続のチャプターは、再生ヘッドの開始時間と一致するオフセットを持っています。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.chapter.offset` |
| **XDM コレクションフィールド** | [`mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.chapter.offset` |
| **必須** | いいえ（モバイル SDK）；はい（Edge、Media Collection API） |
| **様が**&#x200B;様と共に送信されました | [章の開始](/help/implementation/events/chapters/chapter-start.md)、章の終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.chapterDetails`内に`offset`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Act II",
        index: 2,
        offset: 240,
        length: 360
      },
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## モバイル SDK

オフセットを4番目の引数（`startTime`）として`createChapterObject`に渡します。

**iOS （Swift）**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android （Kotlin）**

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku （BrightScript）

`media.chapterStart`の`sendMediaEvent`を呼び出す場合、`mediaCollection.chapterDetails`内に`offset`を設定します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Act II",
                "index": 2,
                "offset": 240,
                "length": 360
            },
            "playhead": 240
        }
    }
})
```

## Media Edge API

`mediaCollection.chapterDetails`内の`offset`で[chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) エンドポイントを呼び出します。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "index": 2,
          "offset": 240,
          "length": 360
        },
        "sessionID": "{sid}",
        "playhead": 240
      }
    }
  }]
}
```

## メディア SDK

オフセットを4番目の引数として`ADB.Media.createChapterObject`に渡します。

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Act II",
  2,
  360,
  240
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## メディアコレクション API

`chapterStart` POST リクエストの`params` オブジェクトに`media.chapter.offset`を含めます：

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.offset": 240
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
