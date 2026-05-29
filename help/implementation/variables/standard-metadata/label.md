---
title: ラベル
description: オーディオコンテンツをリリースしたレコードラベルを設定します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 10%

---


# ラベル

>[!BEGINSHADEBOX]

*このページでは、**Label**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; ラベル &#x200B;](/help/reporting/dimensions/label.md)を参照してください。*

>[!ENDSHADEBOX]

ラベル変数は、オーディオコンテンツをリリースしたレコードラベルの名前です（例：`"Capitol Records"`）。 音楽またはポッドキャストカタログのラベル間でエンゲージメントを比較するために使用します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.label` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.sessionDetails.label`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.label` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [&#x200B; セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.sessionDetails`内に`label`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        label: "Capitol Records"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

HashMap引数のメタデータ キーとしてラベルを`trackSessionStart`に渡します。 `MediaConstants.AudioMetadataKeys.LABEL`.を使用します。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.LABEL] = "Capitol Records"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

HashMap引数のメタデータ キーとしてラベルを`trackSessionStart`に渡します。 `MediaConstants.AudioMetadataKeys.LABEL`.を使用します。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.LABEL] = "Capitol Records"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

`createMediaSession`を使用して`sessionDetails`内に`label`を設定します：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "label": "Capitol Records"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.sessionDetails`内の`label`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
          "label": "Capitol Records"
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

`ADB.Media.AudioMetadataKeys.Label`を使用して`contextData` オブジェクトにラベルを渡します：

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Label] = "Capitol Records";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

`ADBMobile.media.AudioMetadataKeys.LABEL`を使用して、`trackSessionStart`を呼び出す前に、メディアオブジェクトの`StandardMediaMetadata` プロパティにレコードラベルを設定します。

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.LABEL] = "Capitol Records";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Media Collection API]

`params` オブジェクトに`media.label`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.label": "Capitol Records"
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。

>[!ENDTABS]
