---
title: ビットレートの変更
description: プレーヤーが別のビットレートに切り替えるたびに、ビットレート変更イベントを起動します。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 11%

---


# ビットレートの変更

>[!BEGINSHADEBOX]

*このページでは、ビットレート変更イベントの実装方法について説明します。 対応するレポート変数については、[ ビットレート変更（ディメンション） ](/help/reporting/dimensions/bitrate-changes.md)および[ ビットレート変更（指標） ](/help/reporting/metrics/bitrate-changes.md)を参照してください。*

>[!ENDSHADEBOX]

ビットレート変更イベントは、プレーヤーが別のビットレートに切り替えたことを示します。 最初にQoE オブジェクトの[ ビットレート ](/help/implementation/variables/quality/bitrate.md)値を更新してから、ビットレート変更イベントを実行します。 バックエンドでは、これらのイベントの数を使用して、ビットレートの変更ディメンションと指標を計算し、結果として得られるビットレート値は平均ビットレートを供給します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | （なし – バックエンドでカウント） |
| **XDM イベントタイプ** | `media.bitrateChange` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | プレイヤーがビットレートを切り替えるたびに |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を使用して、新しいビットレートで`media.bitrateChange` イベントを送信します。

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 4500,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 120
    }
  }
});
```

## モバイル SDK

新しいビットレートでQoE オブジェクトを更新し、ビットレート変更イベントを実行します。

**iOS （Swift）**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android （Kotlin）**

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku （BrightScript）

`sendMediaEvent`と`media.bitrateChange`を使用して、ビットレートの変更を通知します。 `qoeDataDetails`に新しいビットレートを含めます：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 4500,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 120
        }
    }
})
```

## Media Edge API

更新された`qoeDataDetails`で[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) エンドポイントを呼び出します。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 4500
        },
        "sessionID": "{sid}",
        "playhead": 120
      }
    }
  }]
}
```

## メディア SDK

QoE オブジェクトを更新し、イベントを実行します。

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## メディアコレクション API

新しいビットレートで`bitrateChange` POST リクエストを送信します。

```json
{
  "playerTime": { "playhead": 120, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 4500
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
