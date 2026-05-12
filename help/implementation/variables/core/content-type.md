---
title: コンテンツタイプ
description: コンテンツの種類を設定して、ストリームのフォーマット（VOD、ライブ、リニア、ポッドキャスト、曲など）を特定します。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 10%

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
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必須** | はい |
| **様が**&#x200B;様と共に送信されました | セッション開始、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内に`contentType`を設定：

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

## モバイル SDK

コンテンツタイプ定数を`streamType`引数として`createMediaObject`に渡します。 `VOD`、`LIVE`、`LINEAR`、`AOD`、`PODCAST`など、`MediaConstants.StreamType.*`個の値を使用します。 注意：Mobile SDKでは、`streamType`引数でContent Typeが制御されます。 ストリームタイプ変数（オーディオとビデオの比較）は、別の`mediaType`引数です。

**iOS （Swift）**

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android （Kotlin）**

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku （BrightScript）

`createMediaSession`の呼び出し時に`mediaCollection.sessionDetails`内に`contentType`を設定：

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

## Media Edge API

`mediaCollection.sessionDetails`内の`contentType`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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

## メディア SDK

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

## メディアコレクション API

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
