---
title: コンテンツ名
description: コンテンツのわかりやすい名前（レポートに表示される人間が読めるタイトル）を設定します。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 8%
---

# コンテンツ名

>[!BEGINSHADEBOX]

*このページでは、**コンテンツ名**変数のデータ収集について説明します。 対応するレポートディメンションについては、[ コンテンツ名](/help/reporting/dimensions/content-name.md)を参照してください。*

>[!ENDSHADEBOX]

コンテンツ名変数は、人間が読み取れるコンテンツのタイトルです（例：`"Blinding Light"`）。 オプションですが、強くお勧めします。 XDM スキーマでは、`friendlyName`にマッピングされます（`name`ではなく、`name`はコンテンツ IDを保持します）。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.friendlyName` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.friendlyName` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [ セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`friendlyName`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "Blinding Light",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

最初の（`name`）引数として人間が読み取れる名前を`createMediaObject`に渡します。 2番目の引数はコンテンツ IDです。

```swift
let mediaObject = Media.createMediaObjectWith(name: "Blinding Light",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

最初の（`name`）引数として人間が読み取れる名前を`createMediaObject`に渡します。 2番目の引数はコンテンツ IDです。

```kotlin
var mediaInfo = Media.createMediaObject("Blinding Light",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Edge六]

`createMediaSession`の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`friendlyName`を設定：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "Blinding Light",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.sessionDetails`内の`friendlyName`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "friendlyName": "Blinding Light",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports"
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

最初の引数として人間が読み取れる名前を`ADB.Media.createMediaObject`に渡します：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "Blinding Light",    // name (friendly name)
  "video-123",              // media ID
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

最初の引数として人間が読み取れる名前を`ADBMobile.media.createMediaObject`に渡します：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "Blinding Light",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

最初の引数として人間が読み取れる名前を`adb_media_init_mediainfo`に渡します：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Blinding Light", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB Media Collection API]

`sessionStart` POST リクエストの`params` オブジェクトに`media.name`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.name": "Blinding Light"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス ](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions)を参照してください。

>[!ENDTABS]
