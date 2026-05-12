---
title: ビットレート
description: バックエンドがビットレート指標を計算できるように、QoE オブジェクトの現在の再生ビットレート（kbps）を設定します。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 10%

---


# ビットレート

>[!BEGINSHADEBOX]

*このページでは、**ビットレート**&#x200B;変数のデータ収集について説明します。 対応するレポート変数については、[平均ビットレート （ディメンション） &#x200B;](/help/reporting/dimensions/average-bitrate.md)および[平均ビットレート （指標） &#x200B;](/help/reporting/metrics/average-bitrate.md)を参照してください。*

>[!ENDSHADEBOX]

ビットレート変数は、現在の再生ビットレート（キロビット/秒）です。 プレーヤーがビットレートを交渉するたびにQoE オブジェクトに設定し、ビットレートが変更されたときにQoE オブジェクトを更新します。 バックエンドでは、ビットレート値を使用して、平均ビットレート、ビットレート単位バケット単位のディメンション、ビットレート変更指標を計算します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.qoe.bitrateAverageBucket` |
| **XDM コレクションフィールド** | [`mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | 品質イベント（ビットレート変更、バッファー、エラー）、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を呼び出す際、`media.bitrateChange` （または品質関連のイベント）に`bitrate`を`mediaCollection.qoeDataDetails`内に設定します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## モバイル SDK

ビットレートを最初の引数として`createQoEObject`に渡します。 品質イベントが発生する前に、トラッカー上のQoE オブジェクトを更新します。

**iOS （Swift）**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android （Kotlin）**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku （BrightScript）

`media.bitrateChange`などの品質イベントに`sendMediaEvent`を呼び出す場合、`mediaCollection.qoeDataDetails`内に`bitrate`を設定します。

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

`mediaCollection.qoeDataDetails`内の`bitrate`で[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) エンドポイントを呼び出します：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## メディア SDK

ビットレートを最初の引数として`ADB.Media.createQoEObject`に渡し、トラッカーを更新します。

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
```

## メディアコレクション API

`bitrateChange` POST リクエストの`params` オブジェクトに`media.qoe.bitrate`を含めます：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 3200
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
