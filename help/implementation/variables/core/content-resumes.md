---
title: コンテンツの再開
description: バックエンドがコンテンツ再開イベントをカウントするように、以前に中断された再生を再開するセッションにフラグを付けます。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 11%

---


# コンテンツの再開

>[!BEGINSHADEBOX]

*このページでは、**Content resumes**変数のデータ収集について説明します。 対応するレポート指標については、[ コンテンツの再開](/help/reporting/metrics/content-resumes.md)を参照してください。*

>[!ENDSHADEBOX]

コンテンツは、以前に中断された再生を再開するセッションに変数フラグを付けます。 バックエンドがセッションのコンテンツ再開イベントをカウントし、新しいストリームのカウントから除外するように、`media.sessionStart`に設定します。 ダイレクト APIおよびEdge APIの実装の場合、クライアントは再開されたセッションを検出し（例えば、バッファ、一時停止、または30分を超える停止の後）、それに応じてこのフラグを設定する責任があります。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.resume` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | 該当なし |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [ セッション開始](/help/implementation/events/session/session-start.md) |

## Web SDK

`hasResume`を`mediaCollection.sessionDetails`内の`true`に設定し、再開されたセッションの[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を呼び出します。

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
        streamType: "video",
        hasResume: true
      },
      playhead: 60
    }
  }
});
```

## モバイル SDK

`trackSessionStart`で、メディアオブジェクトのオプションの設定バンドルの一部として再開フラグを渡します。 `MediaConstants.MediaObjectKey.RESUMED` キーを使用します。

**iOS （Swift）**

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android （Kotlin）**

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

## Roku （BrightScript）

`hasResume`を`mediaCollection.sessionDetails`内の`true`に設定し、再開されたセッションの`createMediaSession`を呼び出します。

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
                "streamType": "video",
                "hasResume": true
            },
            "playhead": 60
        }
    }
})
```

## Media Edge API

`mediaCollection.sessionDetails`内で`hasResume`が`true`に設定された[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "hasResume": true
        },
        "playhead": 60
      }
    }
  }]
}
```

## メディア SDK

`trackSessionStart`を呼び出す前に、メディア情報オブジェクトの`RESUMED` キーを設定します。

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);
mediaInfo[ADB.Media.MediaObjectKey.Resumed] = true;

tracker.trackSessionStart(mediaInfo, contextData);
```

## メディアコレクション API

`sessionStart` POST リクエストの`params` オブジェクトに`media.resume`を含めます：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.resume": true
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
