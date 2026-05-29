---
title: ストリームタイプ
description: ストリームタイプを設定して、メディアストリームがオーディオまたはビデオコンテンツかどうかを識別します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 7%

---


# ストリームタイプ

>[!BEGINSHADEBOX]

*このページでは、**Stream type**変数のデータ収集について説明します。 対応するレポートディメンションについては、[ ストリームタイプ ](/help/reporting/dimensions/stream-type.md)を参照してください。*

>[!ENDSHADEBOX]

ストリームタイプ変数は、メディアストリームがオーディオまたはビデオコンテンツであるかどうかを識別します。 これは、すべてのストリーミングメディア実装に必要であり、すべてのメディアセッションの開始時に設定する必要があります。

ストリームタイプを正しく設定することは、ストリーミングメディアレポートの基礎となります。 Adobe Analyticsの組み込みの&#x200B;**Media Stream Type** セグメント（すべてのメディア、オーディオのみ、ビデオのみ）を有効にし、Customer Journey Analyticsでオーディオとビデオのレポートを個別に作成します。 また、セッションデータがメディア分析パイプライン全体で正しく分類されます。 ストリームタイプが未設定または無効なセッションは、ダウンストリームレポートでグループ化を解除したり、分類を誤ったりする可能性があります。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.streamType` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.streamType` |
| **必須** | はい |
| **様が**&#x200B;様と共に送信されました | [ セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`streamType`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
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

`Media.MediaType.Video`または`Media.MediaType.Audio`を`mediaType`引数として`createMediaObject`に渡します。 `createMediaObject`の`streamType`引数は、この変数ではなく、コンテンツタイプ変数（VOD、Liveなど）を制御することに注意してください。

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                                id: "video-id",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

`Media.MediaType.Video`または`Media.MediaType.Audio`を`mediaType`引数として`createMediaObject`に渡します。 `createMediaObject`の`streamType`引数は、この変数ではなく、コンテンツタイプ変数（VOD、Liveなど）を制御することに注意してください。

```kotlin
var mediaInfo = Media.createMediaObject("video-123",
                                        "video-id",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

`createMediaSession`の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`streamType`を設定：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
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

`xdm.mediaCollection.sessionDetails`内の`streamType`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "streamType": "video"
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

`ADB.Media.MediaType.Video`または`ADB.Media.MediaType.Audio`を5番目の引数として`Media.createMediaObject`に渡します：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name
  "video-123",              // media ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD, // content type
  ADB.Media.MediaType.Video // stream type: Video or Audio
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`ADBMobile.media.MediaType.Video`または`ADBMobile.media.MediaType.Audio`を5番目の引数として`ADBMobile.media.createMediaObject`に渡します：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Media Collection API]

`sessionStart` POST リクエストの`params` オブジェクトに`media.streamType`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamType": "video"
  }
}
```

完全なリクエスト構造とすべての必須フィールドについては、[Media Collection API セッション リファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
