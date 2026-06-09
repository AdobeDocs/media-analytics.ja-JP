---
title: アセット ID
description: アセット IDを設定します。EIDRやTMS/Gracenote IDなどのメディアアセットの安定した業界識別子です。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 8%

---


# アセット ID

>[!BEGINSHADEBOX]

*このページでは、**アセット ID**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; アセット ID](/help/reporting/dimensions/asset-id.md)を参照してください。*

>[!ENDSHADEBOX]

アセット ID変数は、基になるメディアアセットの一意の識別子（エピソード ID、ムービーID、ライブイベント IDなど）です。 通常、EIDR、TMS/Gracenote、Roviなどのメタデータ機関から入手されますが、独自のIDや社内のIDも利用できます。 同じアセットに異なるコンテンツ IDを割り当てる可能性のある配信プラットフォーム間のエンゲージメントを比較する必要がある場合に使用します。

>[!NOTE]
>
>XDM コレクションフィールドでは、大文字の`ID`: `assetID`が使用されます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.asset` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.asset` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`assetID`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        assetID: "89745363"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

アセット IDをHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.ASSET_ID`.を使用します。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

アセット IDをHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.ASSET_ID`.を使用します。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Edge六]

`createMediaSession`を使用して`sessionDetails`内に`assetID`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "assetID": "89745363"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.sessionDetails`内の`assetID`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "assetID": "89745363"
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

`ADB.Media.VideoMetadataKeys.AssetId`を使用して`contextData` オブジェクト内のアセット IDを渡します：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AssetId] = "89745363";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`ADBMobile.media.VideoMetadataKeys.ASSET_ID`を使用して、`trackSessionStart`を呼び出す前に、メディアオブジェクトの`StandardMediaMetadata` プロパティでアセット IDを設定します。

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.ASSET_ID] = "89745363";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

`MEDIA_VideoMetadataKeyASSET_ID`を使用して、`mediaTrackSessionStart`を呼び出す前に、メディアオブジェクトの標準メタデータでアセット IDを設定します。

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyASSET_ID] = "89745363"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`params` オブジェクトに`media.assetId`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.assetId": "89745363"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
