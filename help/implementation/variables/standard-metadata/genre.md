---
title: ジャンル
description: コンテンツジャンルをコンマ区切りの文字列として設定します。 マルチジャンルのコンテンツは、レポートの行項目に分割されます。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 13%

---


# ジャンル

>[!BEGINSHADEBOX]

*このページでは、**ジャンル**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; ジャンル &#x200B;](/help/reporting/dimensions/genre.md)を参照してください。*

>[!ENDSHADEBOX]

ジャンル変数は、プロデューサーが定義したコンテンツジャンルです（例：`"Drama"`、`"Comedy"`、または`"Drama,Action"`）。 コンテンツが複数のジャンルに適合する場合、複数の値をカンマ区切りします。 レポートでは、リスト変数は、各値を個別の行項目に分割し、各行項目に等しい指標の重みを割り当てます。

>[!NOTE]
>
>レポートパイプラインでは、ジャンルの値は`mediaReporting.sessionDetails.genreList` （リストフィールド）として公開されます。 古い`mediaReporting.sessionDetails.genre` パスは引き続き機能しますが、`genreList`をお勧めします。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.genre` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | セッション開始、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内に`genre`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        genre: "Drama,Action"
      },
      playhead: 0
    }
  }
});
```

## モバイル SDK

ジャンル文字列をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.GENRE`.を使用します。

**iOS （Swift）**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android （Kotlin）**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku （BrightScript）

`createMediaSession`を使用して`sessionDetails`内に`genre`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "genre": "Drama,Action"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails`内の`genre`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "genre": "Drama,Action"
        },
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.VideoMetadataKeys.Genre`を使用して`contextData` オブジェクト内のジャンルを渡します：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

## メディアコレクション API

`params` オブジェクトに`media.genre`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.genre": "Drama,Action"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
