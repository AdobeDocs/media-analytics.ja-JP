---
title: コンテンツタイプ
description: コンテンツの種類を設定して、ストリームのフォーマット（VOD、ライブ、リニア、ポッドキャスト、曲など）を特定します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 5%

---


# コンテンツタイプ

>[!BEGINSHADEBOX]

*このページでは、**コンテンツ タイプ**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; コンテンツタイプ &#x200B;](/help/reporting/dimensions/content-type.md)を参照してください。*

>[!ENDSHADEBOX]

コンテンツタイプ変数は、ストリームのフォーマットを指定します（例えば、ビデオの場合はVOD、ライブ、リニア、オーディオの場合はポッドキャストまたはオーディオブック）。 これは、すべてのストリーミングメディア実装に必要であり、セッション開始時に設定する必要があります。 Adobeで定義された値は、組み込みのコンテンツタイプセグメントとレポートに入力されます。カスタム文字列も使用できますが、組み込みのセグメントと一致しません。 未設定の場合、値はデフォルトで`missing_content_type`になります。

推奨値：

* **ビデオ：** `vod`、`live`、`linear`、`ugc`、`dvod`
* **音声：** `song`、`podcast`、`audiobook`、`radio`

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.contentType` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.contentType` |
| **必須** | はい |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`contentType`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
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

コンテンツタイプ定数を`streamType`引数として`createMediaObject`に渡します。 `VOD`、`LIVE`、`LINEAR`、`AOD`、`PODCAST`など、`MediaConstants.StreamType.*`個の値を使用します。 注意：Mobile SDKでは、`streamType`引数でContent Typeが制御されます。 ストリームタイプ変数（オーディオとビデオの比較）は、別の`mediaType`引数です。

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

コンテンツタイプ定数を`streamType`引数として`createMediaObject`に渡します。 `VOD`、`LIVE`、`LINEAR`、`AOD`、`PODCAST`など、`MediaConstants.StreamType.*`個の値を使用します。 注意：Mobile SDKでは、`streamType`引数でContent Typeが制御されます。 ストリームタイプ変数（オーディオとビデオの比較）は、別の`mediaType`引数です。

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

`createMediaSession`の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`contentType`を設定：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
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

`xdm.mediaCollection.sessionDetails`内の`contentType`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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

`ADB.Media.StreamType.*`定数を4番目の引数として`ADB.Media.createMediaObject`に渡します：

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD, // Content type — VOD, LIVE, LINEAR, etc.
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`ADBMobile.media.StreamType.*`定数を4番目の引数として`ADBMobile.media.createMediaObject`に渡します：

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

`sessionStart` POST リクエストの`params` オブジェクトに`media.contentType`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.contentType": "vod"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
