---
title: 日パート
description: コンテンツがブロードキャストまたは再生されたときの時間帯バケット（午前、午後、時間、深夜）を設定します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 8%

---


# 日パート

>[!BEGINSHADEBOX]

*このページでは、**日パート**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[日パート &#x200B;](/help/reporting/dimensions/day-part.md)を参照してください。*

>[!ENDSHADEBOX]

日別パート変数は、コンテンツがブロードキャストまたは再生された時間帯バケットです（例：`"Morning"`、`"Afternoon"`、`"Primetime"`、または`"Late Night"`）。 任意の文字列を使用できます。 視聴者のローカルタイムゾーンに依存せずに、時間帯全体のエンゲージメントを比較するために使用します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.dayPart` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.dayPart` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`dayPart`を設定：

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

>[!TAB iOS]

日付部分をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.DAY_PART`.を使用します。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

日付部分をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.DAY_PART`.を使用します。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.DAY_PART] = "Primetime"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

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

>[!TAB Media Edge API]

`xdm.mediaCollection.sessionDetails`内の`dayPart`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`ADB.Media.VideoMetadataKeys.DayPart`を使用して、`contextData` オブジェクトの日付部分を渡します：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.DayPart] = "Primetime";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`ADBMobile.media.VideoMetadataKeys.DAY_PART`を使用して、`trackSessionStart`を呼び出す前に、メディアオブジェクトの`StandardMediaMetadata` プロパティで日付部分を設定します。

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.DAY_PART] = "Primetime";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Media Collection API]

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

>[!ENDTABS]
