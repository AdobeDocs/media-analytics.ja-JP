---
title: ビットレート
description: バックエンドがビットレート指標を計算できるように、QoE オブジェクトの現在の再生ビットレート（kbps）を設定します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 6%

---


# ビットレート

>[!BEGINSHADEBOX]

*このページでは、**ビットレート**&#x200B;変数のデータ収集について説明します。 対応するレポート変数については、[[!UICONTROL 平均ビットレート &#x200B;] （ディメンション） &#x200B;](/help/reporting/dimensions/average-bitrate.md)および[[!UICONTROL 平均ビットレート &#x200B;] （指標） &#x200B;](/help/reporting/metrics/average-bitrate.md)を参照してください。*

>[!ENDSHADEBOX]

ビットレート変数は、現在の再生ビットレート（キロビット/秒）です。 プレーヤーがビットレートを交渉するたびにQoE オブジェクトに設定し、ビットレートが変更されたときにQoE オブジェクトを更新します。 バックエンドでは、ビットレート値を使用して、[[!UICONTROL 平均ビットレート &#x200B;]](/help/reporting/metrics/average-bitrate.md)、ビットレートごとのバケット ディメンション、[[!UICONTROL &#x200B; ビットレート変更]](/help/reporting/metrics/bitrate-changes.md)指標を計算します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.qoe.bitrateAverageBucket` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.qoe.bitrateAverageBucket` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | 品質イベント （[&#x200B; ビットレート変更](/help/implementation/events/playback/bitrate-change.md)、[&#x200B; バッファー開始](/help/implementation/events/playback/buffer-start.md)、[&#x200B; エラー](/help/implementation/events/error.md)）、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を呼び出す際、`media.bitrateChange` （または品質関連のイベント）に`bitrate`を`xdm.mediaCollection.qoeDataDetails`内に設定します：

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

>[!TAB iOS]

ビットレートを最初の引数として`createQoEObject`に渡します。 品質イベントが発生する前に、トラッカー上のQoE オブジェクトを更新します。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

ビットレートを最初の引数として`createQoEObject`に渡します。 品質イベントが発生する前に、トラッカー上のQoE オブジェクトを更新します。

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

`media.bitrateChange`などの品質イベントに`sendMediaEvent`を呼び出す場合、`xdm.mediaCollection.qoeDataDetails`内に`bitrate`を設定します。

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

>[!TAB Media Edge API]

`xdm.mediaCollection.qoeDataDetails`内の`bitrate`で[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) エンドポイントを呼び出します：

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

ビットレートをkbpsで第1引数として`ADBMobile.media.createQoSObject`に渡し、トラッカーを更新します。

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Media Collection API]

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

>[!ENDTABS]
