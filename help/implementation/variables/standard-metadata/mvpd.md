---
title: MVPD
description: ユーザーがAdobe Passを介して認証する場合は、マルチチャネルビデオプログラミングディストリビューターを設定します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 9%

---


# MVPD

>[!BEGINSHADEBOX]

*このページでは、**MVPD**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[MVPD](/help/reporting/dimensions/mvpd.md)を参照してください。*

>[!ENDSHADEBOX]

MVPD （マルチチャネル ビデオ プログラミング ディストリビューター）変数は、ユーザーが認証を行うケーブル、サテライト、またはバーチャル MVPD プロバイダー（例：`"Comcast"`、`"DirecTV"`、または`"YouTubeTV"`）です。 Adobe PassやTV-Everywhereの認証に依存することなく、コンテンツを配信するタイミングを設定できます。 [Authorized](/help/implementation/variables/standard-metadata/authorized.md)と組み合わせて、認証を完了したセッションを追跡します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.pass.mvpd` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.pass.mvpd` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`mvpd`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        mvpd: "Comcast"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

MVPDをHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.MVPD`.を使用します。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

MVPDをHashMap引数のメタデータキーとして`trackSessionStart`に渡します。 `MediaConstants.VideoMetadataKeys.MVPD`.を使用します。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

`createMediaSession`を使用して`sessionDetails`内に`mvpd`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "mvpd": "Comcast"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.sessionDetails`内の`mvpd`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "mvpd": "Comcast"
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

`ADB.Media.VideoMetadataKeys.MVPD`を使用して、`contextData` オブジェクトにMVPDを渡します。

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.MVPD] = "Comcast";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`ADBMobile.media.VideoMetadataKeys.MVPD`を使用して、`trackSessionStart`を呼び出す前に、メディアオブジェクトの`StandardMediaMetadata` プロパティでMVPDを設定します。

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "Comcast";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Media Collection API]

`params` オブジェクトに`media.pass.mvpd`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.mvpd": "Comcast"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
