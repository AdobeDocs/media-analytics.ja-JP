---
title: コンテンツチャネル
description: コンテンツが再生される配信ステーション、ネットワーク、またはプロパティを識別するチャネルを設定します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 7%

---


# コンテンツチャネル

>[!BEGINSHADEBOX]

*このページでは、**コンテンツチャネル**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; コンテンツチャネル &#x200B;](/help/reporting/dimensions/content-channel.md)を参照してください。*

>[!ENDSHADEBOX]

コンテンツチャネル変数は、コンテンツが再生される配信ステーション、ネットワーク、またはプロパティを識別します。 すべてのストリーミングメディア実装に必要です。 任意の文字列を使用できます。 一般的な値には、ネットワーク名、サイトパスの一部、内部プロパティ識別子などがあります。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.channel` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.channel`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.channel` |
| **必須** | はい |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`channel`を設定：

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

`MediaConstants.TrackerConfig.CHANNEL`を使用してトラッカーを作成する際に、トラッカー設定を通じてチャネルを設定します。 チャネルはメディアオブジェクトの一部ではありません。

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

`MediaConstants.TrackerConfig.CHANNEL`を使用してトラッカーを作成する際に、トラッカー設定を通じてチャネルを設定します。 チャネルはメディアオブジェクトの一部ではありません。

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

>[!TAB Roku]

`createMediaSession`の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`channel`を設定：

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

`xdm.mediaCollection.sessionDetails`内の`channel`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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

トラッカーを作成する前に、`ADB.MediaConfig`にチャネルを設定します。

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

`trackSessionStart`の呼び出し時に`channel`を標準メタデータキーとして渡します：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var metadata = { "a.media.channel": "Sports" };
ADBMobile.media.trackSessionStart(mediaInfo, metadata);
```

>[!TAB Media Collection API]

`sessionStart` POST リクエストの`params` オブジェクトに`media.channel`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
