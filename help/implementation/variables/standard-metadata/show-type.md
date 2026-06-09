---
title: タイプを表示
description: 文字列整数コードを使用して、コンテンツ形式（完全なエピソード、プレビュー、クリップなど）を特定します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 7%

---


# タイプを表示

>[!BEGINSHADEBOX]

*このページでは、**Show type**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; タイプを表示](/help/reporting/dimensions/show-type.md)を参照してください。*

>[!ENDSHADEBOX]

show type変数は、文字列整数コードを使用してコンテンツ形式を識別します。

* `"0"`：完全なエピソード
* `"1"`: プレビューまたは予告編
* `"2"`: クリップ
* `"3"`：その他

このツールを使用すると、エンゲージメントを測定する際に、トレーラーやクリップなどの短編コンテンツからプログラム全体の表示を分離できます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.type` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.showType`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.type` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`showType`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        showType: "0"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

HashMap引数のshow typeをメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.SHOW_TYPE`.を使用します。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW_TYPE] = "0"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

HashMap引数のshow typeをメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.SHOW_TYPE`.を使用します。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW_TYPE] = "0"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Edge六]

`createMediaSession`を使用して`sessionDetails`内に`showType`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "showType": "0"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.sessionDetails`内の`showType`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "showType": "0"
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

`ADB.Media.VideoMetadataKeys.ShowType`を使用して、`contextData` オブジェクトに表示タイプを渡します：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.ShowType] = "0";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`ADBMobile.media.VideoMetadataKeys.SHOW_TYPE`を使用して、`trackSessionStart`を呼び出す前に、メディアオブジェクトの`StandardMediaMetadata` プロパティで表示タイプを設定します。

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "0";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

`MEDIA_VideoMetadataKeySHOW_TYPE`を使用して、`mediaTrackSessionStart`を呼び出す前に、メディアオブジェクトの標準メタデータで表示タイプを設定します。

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeySHOW_TYPE] = "0"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`params` オブジェクトに`media.showType`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.showType": "0"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
