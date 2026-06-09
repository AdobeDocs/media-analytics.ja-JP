---
title: コンテンツプレーヤー名
description: コンテンツをレンダリングしたプレーヤーを識別するには、プレーヤー名を設定します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 6%

---


# コンテンツプレーヤー名

>[!BEGINSHADEBOX]

*このページでは、**コンテンツプレーヤー名**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; コンテンツプレーヤー名](/help/reporting/dimensions/content-player-name.md)を参照してください。*

>[!ENDSHADEBOX]

コンテンツプレーヤー名変数は、コンテンツをレンダリングしたプレーヤー（`HTML5 Player`、`Brightcove`、または`Roku Player`など）を識別します。 これは、すべてのストリーミングメディア実装に必要であり、セッション開始時に設定する必要があります。 この値は、コンテンツプレーヤー名ディメンションで使用され、同じプロパティのプレーヤー間のエンゲージメントと品質を比較します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.playerName` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.playerName` |
| **必須** | はい |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`playerName`を設定：

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

`MediaConstants.TrackerConfig.PLAYER_NAME`を使用してトラッカーを作成する際に、トラッカー設定を使用してプレーヤー名を設定します。 プレーヤー名はメディアオブジェクトの一部ではありません。

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

`MediaConstants.TrackerConfig.PLAYER_NAME`を使用してトラッカーを作成する際に、トラッカー設定を使用してプレーヤー名を設定します。 プレーヤー名はメディアオブジェクトの一部ではありません。

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

>[!TAB Edge六]

`createMediaSession`の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`playerName`を設定：

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

`xdm.mediaCollection.sessionDetails`内の`playerName`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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

トラッカーを作成する前に、`ADB.MediaConfig`でプレーヤー名を設定します。

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

`trackSessionStart`を呼び出す際に、プレーヤー名を標準メタデータキーとして渡します：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var metadata = { "a.media.playerName": "Chromecast Player" };
ADBMobile.media.trackSessionStart(mediaInfo, metadata);
```

>[!TAB Roku 2.x]

`ADBMobileConfig.json`の`mediaHeartbeat` セクションで`playerName`を設定します。 プレーヤー名は設定値であり、セッションごとの値ではありません。

```json
"mediaHeartbeat": {
  "playerName": "Roku Player"
}
```

>[!TAB Media Collection API]

`sessionStart` POST リクエストの`params` オブジェクトに`media.playerName`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "HTML5 Player"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
