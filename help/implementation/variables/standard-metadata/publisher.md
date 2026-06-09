---
title: 発行者
description: オーディオコンテンツパブリッシャーを設定します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 9%

---


# 発行者

>[!BEGINSHADEBOX]

*このページでは、**Publisher**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[発行者](/help/reporting/dimensions/publisher.md)を参照してください。*

>[!ENDSHADEBOX]

パブリッシャー変数は、オーディオコンテンツパブリッシャーの名前（例：ポッドキャストネットワークまたはオーディオブックパブリッシャー）です。 厳選されたオーディオカタログで、メディア企業間のエンゲージメントを比較するために使用できます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.publisher` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.publisher`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.publisher` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`publisher`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        publisher: "Northbridge Audio"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

発行者をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.AudioMetadataKeys.PUBLISHER`.を使用します。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

発行者をHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.AudioMetadataKeys.PUBLISHER`.を使用します。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Edge六]

`createMediaSession`を使用して`sessionDetails`内に`publisher`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "publisher": "Northbridge Audio"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.sessionDetails`内の`publisher`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "publisher": "Northbridge Audio"
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

`ADB.Media.AudioMetadataKeys.Publisher`を使用して`contextData` オブジェクト内の発行者を渡します：

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Publisher] = "Northbridge Audio";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`ADBMobile.media.AudioMetadataKeys.PUBLISHER`を使用して、`trackSessionStart`を呼び出す前に、メディア オブジェクトの`StandardMediaMetadata` プロパティで発行者を設定します。

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.PUBLISHER] = "Northbridge Audio";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

`MEDIA_AudioMetadataKeyPUBLISHER`を使用して、`mediaTrackSessionStart`を呼び出す前に、メディア オブジェクトの標準メタデータで発行者を設定します。

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Track", "audio-123", 240.0, adb.MEDIA_STREAM_TYPE_AOD, adb.MEDIA_TYPE_AUDIO)

standardMetadata = {}
standardMetadata[adb.MEDIA_AudioMetadataKeyPUBLISHER] = "Northbridge Audio"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`params` オブジェクトに`media.publisher`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.publisher": "Northbridge Audio"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
