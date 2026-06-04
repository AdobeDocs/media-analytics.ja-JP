---
title: アプリバージョン
description: メディアプレーヤーアプリケーションのバージョン文字列を設定します。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---


# アプリバージョン

>[!BEGINSHADEBOX]

*このページでは、**アプリ バージョン**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; アプリバージョン &#x200B;](/help/reporting/dimensions/app-version.md)を参照してください。*

>[!ENDSHADEBOX]

アプリのバージョン変数は、メディアプレーヤーアプリケーションのバージョンを識別します。 SDKの初期化中に1回設定します。この値は、以降のすべてのセッション開始リクエストに自動的に含まれます。 アプリケーションのリリースサイクルに一致するバージョン文字列を使用します（例：`"2.1.0"`または`"prod-YYYY-03-15"`）。

>[!NOTE]
>
>このフィールドは、AdobeのSDK ライブラリではなく、**media player アプリケーション**&#x200B;のバージョンをキャプチャします。 Adobe独自のSDK ライブラリバージョンは、個別の内部フィールドとして自動的に収集されます。

| プロパティ | 値 |
| --- | --- |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.appVersion`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Media Collection API パラメーター** | `media.sdkVersion` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md) |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`configure`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/configure/streamingmedia)の呼び出し時に`streamingMedia`設定オブジェクトに`appVersion`を設定します：

```javascript
alloy("configure", {
  streamingMedia: {
    channel: "Sports Channel",
    playerName: "HTML5 Player",
    appVersion: "2.1.0",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

>[!TAB iOS]

メディアトラッカーを初期化する前に、アプリ設定で`edgeMedia.appVersion`を設定します。

```swift
var config: [String: Any] = [:]
config["edgeMedia.channel"] = "sample_channel"
config["edgeMedia.playerName"] = "player_name"
config["edgeMedia.appVersion"] = "2.1.0"
MobileCore.updateConfiguration(config)
```

>[!TAB Android]

メディアトラッカーを初期化する前に、アプリ設定で`edgeMedia.appVersion`を設定します。

```kotlin
val config: Map<String, Any> = mapOf(
    "edgeMedia.channel" to "sample_channel",
    "edgeMedia.playerName" to "player_name",
    "edgeMedia.appVersion" to "2.1.0"
)
MobileCore.updateConfiguration(config)
```

>[!TAB Roku]

`ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION`を使用して、SDK設定でアプリのバージョンを設定します。

```brightscript
ADB_CONSTANTS = AdobeAEPSDKConstants()
configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<YOUR_CONFIG_ID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "channel_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION] = "2.1.0"
m.aepSdk.updateConfiguration(configuration)
```

>[!TAB Media Edge API]

[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)要求の`sessionDetails` オブジェクトに`appVersion`を含めます：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "appVersion": "2.1.0"
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

`ADB.Media.configure`を呼び出す前に、`MediaConfig` オブジェクトに`appVersion`を設定します：

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "2.1.0";
ADB.Media.configure(mediaConfig, appMeasurement);
```

>[!TAB Chromecast]

ADBMobile設定の`mediaHeartbeat` セクションで`sdkVersion`を設定します。 このフィールドは、Chromecast SDK ライブラリのバージョンではなく、Player アプリケーションのバージョンをキャプチャします。

```javascript
var ADBMobileConfig = {
  "mediaHeartbeat": {
    "server": "obumobile5.hb-api.omtrdc.net",
    "publisher": "<YOUR_PUBLISHER_ID>@AdobeOrg",
    "channel": "sample-channel",
    "ssl": true,
    "playerName": "Chromecast Player",
    "sdkVersion": "2.1.0"
  }
};
```

>[!TAB Media Collection API]

`sessionStart` POST リクエストの`params` オブジェクトに`media.sdkVersion`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "sample-html5-api-player",
    "media.sdkVersion": "2.1.0",
    "media.channel": "sample-channel"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
