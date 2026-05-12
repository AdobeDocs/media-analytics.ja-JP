---
title: コンテンツの長さ
description: セッション開始時にコンテンツの長さを秒単位で設定します。 これにより、進捗状況マーカーと毎分平均オーディエンス数を向上できます。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 12%

---


# コンテンツの長さ

>[!BEGINSHADEBOX]

*このページでは、**コンテンツの長さ**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; コンテンツの長さ](/help/reporting/dimensions/content-length.md)を参照してください。*

>[!ENDSHADEBOX]

コンテンツの長さ変数は、コンテンツの合計時間（秒単位）です。 これは、すべてのストリーミングメディア実装に必要であり、セッション開始時に設定する必要があります。 コンテンツの長さは、進捗状況マーカー（10/25/50/75/95%）や毎分平均オーディエンスなど、バックエンドで計算された複数の指標を促進します。 コンテンツの長さが設定されていないか、ゼロより大きくない場合、これらの指標は生成されません。 期間が不明なライブストリームの場合は、`86400` （24時間）を使用します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.length` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **必須** | はい |
| **様が**&#x200B;様と共に送信されました | セッション開始、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内に`length`を設定：

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

コンテンツの長さを`length`引数として`createMediaObject`に秒単位で渡します。

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

`createMediaSession`の呼び出し時に`mediaCollection.sessionDetails`内に`length`を設定：

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

## Media Edge API

`mediaCollection.sessionDetails`内の`length`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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

コンテンツの長さを3番目の引数として`ADB.Media.createMediaObject`に秒単位で渡します。

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,                      // length in seconds
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## メディアコレクション API

`sessionStart` POST リクエストの`params` オブジェクトに`media.length`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.length": 128
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
