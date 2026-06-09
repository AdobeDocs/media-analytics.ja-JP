---
title: 最初のデジタル日付
description: デジタルプラットフォームでコンテンツが最初に放映される日付を設定します。 Adobeでは、YYY-MM-DD形式を推奨しています。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 7%

---


# 最初のデジタル日付

>[!BEGINSHADEBOX]

*このページでは、**最初のデジタル日付**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[最初のデジタル日付](/help/reporting/dimensions/first-digital-date.md)を参照してください。*

>[!ENDSHADEBOX]

最初のデジタル日付変数は、デジタルプラットフォームでコンテンツが最初に放送された日付です。 任意の日付フォーマットを使用できますが、Adobeでは一貫性を保つために`YYYY-MM-DD`を推奨しています。 [最初の放送日](/help/implementation/variables/standard-metadata/first-air-date.md)と同時に使用すると、デジタルリリースのタイミングと元の放送を比較できます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.digitalDate` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.digitalDate` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`firstDigitalDate`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstDigitalDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

最初のデジタル日付をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE`.を使用します。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

最初のデジタル日付をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE`.を使用します。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Edge六]

`createMediaSession`を使用して`sessionDetails`内に`firstDigitalDate`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstDigitalDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.sessionDetails`内の`firstDigitalDate`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "firstDigitalDate": "2016-01-25"
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

`ADB.Media.VideoMetadataKeys.FirstDigitalDate`を使用して、`contextData` オブジェクトの最初のデジタル日付を渡します：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstDigitalDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE`を使用して、`trackSessionStart`を呼び出す前に、メディアオブジェクトの`StandardMediaMetadata` プロパティで最初のデジタル日付を設定します。

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

`MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE`を使用して、`mediaTrackSessionStart`を呼び出す前に、メディアオブジェクトの標準メタデータで最初のデジタル日付を設定します。

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE] = "2016-01-25"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`params` オブジェクトに`media.firstDigitalDate`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstDigitalDate": "2016-01-25"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
