---
title: ドロップしたフレーム
description: バックエンドがフレームドロップの品質を報告できるように、QoE オブジェクトにドロップされたフレームの実行回数を設定します。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 12%

---


# ドロップしたフレーム

>[!BEGINSHADEBOX]

*このページでは、**削除されたフレーム**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションと指標については、[削除されたフレーム &#x200B;](/help/reporting/dimensions/dropped-frames.md)を参照してください。*

>[!ENDSHADEBOX]

ドロップされたフレーム変数は、セッション中にプレイヤーがドロップしたフレームのランニングカウントです。 QoE オブジェクトに設定し、プレイヤーが新しいドロップを報告するたびに値を更新します。 バックエンドは、セッションのクローズ時に最新の値をレポートします。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.qoe.droppedFrameCount` |
| **XDM コレクションフィールド** | [`mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | 品質イベント、セッション終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.qoeDataDetails`内に`droppedFrames`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## モバイル SDK

4番目の引数としてドロップしたフレームを`createQoEObject`に渡します。 品質イベントが発生する前に、トラッカーを更新します。

**iOS （Swift）**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android （Kotlin）**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

## Roku （BrightScript）

`sendMediaEvent`の呼び出し時に`mediaCollection.qoeDataDetails`内に`droppedFrames`を設定：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

## Media Edge API

`mediaCollection.qoeDataDetails`内の`droppedFrames`で[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) エンドポイントを呼び出します：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## メディア SDK

ドロップしたフレームを4番目の引数として`ADB.Media.createQoEObject`に渡します。

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

## メディアコレクション API

`params` オブジェクトに`media.qoe.droppedFrames`を含めます：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
