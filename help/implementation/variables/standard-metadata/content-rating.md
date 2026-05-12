---
title: コンテンツの評価
description: テレビの保護者のガイドラインまたは地域の評価システムで定義されているコンテンツの評価を設定します。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 14%

---


# コンテンツの評価

>[!BEGINSHADEBOX]

*このページでは、**コンテンツ評価**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; コンテンツの評価](/help/reporting/dimensions/content-rating.md)を参照してください。*

>[!ENDSHADEBOX]

コンテンツの評価の変数は、テレビの保護者のガイドライン （`"TVY"`、`"TVG"`、`"TVPG"`、`"TVMA"`）または使用している地域の評価システムによって定義される視聴者の評価です。 これを使用して、評価階層をまたいでエンゲージメントと広告の負荷を比較します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.rating` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.rating`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | セッション開始、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内に`rating`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        rating: "TVPG"
      },
      playhead: 0
    }
  }
});
```

## モバイル SDK

評価をHashMap引数のメタデータ キーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.RATING`.を使用します。

**iOS （Swift）**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android （Kotlin）**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku （BrightScript）

`createMediaSession`を使用して`sessionDetails`内に`rating`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "rating": "TVPG"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails`内の`rating`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "rating": "TVPG"
        },
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.VideoMetadataKeys.Rating`を使用して`contextData` オブジェクトの評価を渡します：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Rating] = "TVPG";

tracker.trackSessionStart(mediaInfo, contextData);
```

## メディアコレクション API

`params` オブジェクトに`media.rating`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.rating": "TVPG"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
