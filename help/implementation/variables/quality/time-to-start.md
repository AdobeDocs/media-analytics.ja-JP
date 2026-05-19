---
title: 開始時間
description: プレーヤーの起動時間をミリ秒単位で設定し、バックエンドが最初のフレームの品質を報告できるようにします。
feature: Streaming Media
role: Developer
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 9%

---


# 開始時間

>[!BEGINSHADEBOX]

*このページでは、**開始時間**変数のデータ収集について説明します。 対応するレポートディメンションと指標については、[開始までの時間](/help/reporting/dimensions/time-to-start.md)を参照してください。*

>[!ENDSHADEBOX]

変数を開始するまでの時間は、再生を開始してから最初のフレームレンダリングまでの経過時間（ミリ秒単位）です。 セッション開始イベントが発生する前に、QoE オブジェクトに設定します。 Adobeは、値を数秒で保存およびレポートします。ミリ秒単位で渡すと、取り込み時にAdobeがコンバージョンします。

>[!IMPORTANT]
>
>プレーヤーがコンテンツフレームのレンダリングを開始したら、`timeToStart`の更新を停止します。 この値は、最初のバッファリングまたは読み込みフェーズで増加する可能性がありますが、再生が開始された時点から固定として扱う必要があります。 最初のフレームレンダリング後に更新を続けると、膨張または不正確な[開始時間](/help/reporting/metrics/time-to-start.md)指標が生成されます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.qoe.timeToStart` |
| **XDM コレクションフィールド** | [`mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.qoe.timeToStart` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [ セッション開始](/help/implementation/events/session/session-start.md)、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`media.sessionStart`の`mediaCollection.qoeDataDetails`内に`timeToStart`を設定：

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
      qoeDataDetails: {
        timeToStart: 30000
      },
      playhead: 0
    }
  }
});
```

## モバイル SDK

起動時間を2番目の引数（`startupTime`）として`createQoEObject`に渡します。

**iOS （Swift）**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android （Kotlin）**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku （BrightScript）

`createMediaSession`の呼び出し時に`media.sessionStart`の`mediaCollection.qoeDataDetails`内に`timeToStart`を設定：

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
            "qoeDataDetails": {
                "timeToStart": 30000
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.qoeDataDetails`内の`timeToStart`で[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) エンドポイントを呼び出します：

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
        "qoeDataDetails": {
          "timeToStart": 30000
        },
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

2番目の引数として開始する時間を`ADB.Media.createQoEObject`に渡します：

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

## メディアコレクション API

`sessionStart`の`params` オブジェクトに`media.qoe.timeToStart`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.qoe.timeToStart": 30000
  }
}
```

完全なリクエスト構造については、[Media Collection API セッションのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)を参照してください。
