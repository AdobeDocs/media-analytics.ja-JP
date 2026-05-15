---
title: メディアのダウンロード済みフラグ
description: ダウンロードされたオフライン再生としてセッションにマークを付けると、ストリーミングセッションとは別にレポートされます。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 10%

---


# メディアのダウンロード済みフラグ

>[!BEGINSHADEBOX]

*このページでは、**メディア ダウンロード フラグ**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; ダウンロードされたメディア &#x200B;](/help/reporting/dimensions/media-downloaded-flag.md)を参照してください。*

>[!ENDSHADEBOX]

メディアダウンロード済みフラグは、セッションが、インターネットからのライブストリームではなく、以前にダウンロードしたオフラインコンテンツの再生であることを示します。 トラッカー（モバイル SDK）を初期化する際に設定するか、`sessionStart` ペイロード（Edge / Media Collection API）に含めます。 このフラグを使用すると、レポートでストリーミングセッションからオフライン再生を分離できます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.downloaded` |
| **XDM コレクションフィールド** | [`mediaCollection.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.downloaded` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.sessionDetails`内の`isDownloaded`を`true`に設定：

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
        isDownloaded: true
      },
      playhead: 0
    }
  }
});
```

## モバイル SDK

`MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`を使用してトラッカーを作成する際に、トラッカー設定でダウンロード済みコンテンツ フラグを設定します。

**iOS （Swift）**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

**Android （Kotlin）**

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

val tracker = Media.createTracker(config)
```

## Roku （BrightScript）

`createMediaSession`の呼び出し時に`mediaCollection.sessionDetails`内の`isDownloaded`を`true`に設定：

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
                "isDownloaded": true
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

デバイスがオンラインに戻った後、[&#x200B; ダウンロード済み](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/#downloaded) エンドポイントを呼び出し、`mediaDownloadedEvents`内で完全なオフラインセッションをバッチ処理します。 Adobeは自動的に`isDownloaded`を`true`に設定し、セッション IDを割り当てます。ペイロードに含めないでください。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.downloaded",
      "mediaDownloadedEvents": [
        {
          "mediaEventTimestamp": "YYYY-09-26T15:52:24+00:00",
          "mediaEventType": "media.sessionStart",
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
        },
        {
          "mediaEventTimestamp": "YYYY-09-26T15:54:32+00:00",
          "mediaEventType": "media.sessionComplete",
          "mediaCollection": {
            "playhead": 128
          }
        }
      ]
    }
  }]
}
```

## メディア SDK

トラッカーを作成する前に、`ADB.MediaConfig`に`downloadedContent`を設定します：

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";
mediaConfig.downloadedContent = true;

var tracker = ADB.Media.getInstance(mediaConfig);
```

## メディアコレクション API

`sessionStart` POST リクエストの`params` オブジェクトに`media.downloaded`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.downloaded": true
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
