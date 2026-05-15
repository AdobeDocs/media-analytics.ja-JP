---
title: 初回放送日
description: テレビで最初に放映されたコンテンツの日付を設定します。 Adobeでは、YYY-MM-DD形式を推奨しています。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 13%

---


# 初回放送日

>[!BEGINSHADEBOX]

*このページでは、**最初の空気日**変数のデータ収集について説明します。 対応するレポート ディメンションについては、[最初のエア日付](/help/reporting/dimensions/first-air-date.md)を参照してください。*

>[!ENDSHADEBOX]

最初のエア日付変数は、コンテンツが最初にテレビで放映された日付です。 任意の日付フォーマットを使用できますが、Adobeでは一貫性を保つために`YYYY-MM-DD`を推奨しています。 このツールを使用して、新しいリリースのエンゲージメントとカタログコンテンツを比較しています。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.airDate` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.airDate` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [ セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内に`firstAirDate`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstAirDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

## モバイル SDK

HashMap引数のメタデータキーとして、最初のエア日付を`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE`.を使用します。

**iOS （Swift）**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android （Kotlin）**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku （BrightScript）

`createMediaSession`を使用して`sessionDetails`内に`firstAirDate`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstAirDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails`内の`firstAirDate`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "firstAirDate": "2016-01-25"
        },
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.VideoMetadataKeys.FirstAirDate`を使用して、`contextData` オブジェクトの最初のエア日付を渡します：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstAirDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

## メディアコレクション API

`params` オブジェクトに`media.firstAirDate`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstAirDate": "2016-01-25"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
