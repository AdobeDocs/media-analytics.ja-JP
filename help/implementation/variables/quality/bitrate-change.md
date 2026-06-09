---
title: ビットレートの変更
description: プレーヤーが別のビットレートに切り替えるたびに、ビットレート変更イベントを起動します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 6%

---


# ビットレートの変更

>[!BEGINSHADEBOX]

*このページでは、ビットレート変更イベントの実装方法について説明します。 対応するレポート変数については、[[!UICONTROL &#x200B; ビットレート変更] （ディメンション） &#x200B;](/help/reporting/dimensions/bitrate-changes.md)および[[!UICONTROL &#x200B; ビットレート変更] （指標） &#x200B;](/help/reporting/metrics/bitrate-changes.md)を参照してください。*

>[!ENDSHADEBOX]

ビットレート変更イベントは、プレーヤーが別のビットレートに切り替えたことを示します。 最初にQoE オブジェクトの[&#x200B; ビットレート &#x200B;](/help/implementation/variables/quality/bitrate.md)値を更新してから、ビットレート変更イベントを実行します。 バックエンドでは、これらのイベントのカウントを使用して、[[!UICONTROL &#x200B; ビットレート変更]](/help/reporting/dimensions/bitrate-changes.md) ディメンションと[[!UICONTROL &#x200B; ビットレート変更]](/help/reporting/metrics/bitrate-changes.md)指標を計算し、結果のビットレート値は[[!UICONTROL 平均ビットレート &#x200B;]](/help/reporting/metrics/average-bitrate.md)を入力します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | （なし – バックエンドでカウント） |
| **XDM イベントタイプ** | `media.bitrateChange` |
| **Audience Manager特性** | `c_contextdata.a.media.qoe.bitrateChangeCount` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [&#x200B; ビットレート変更](/help/implementation/events/playback/bitrate-change.md) |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

新しいビットレートでQoE オブジェクトを更新し、ビットレート変更イベントを実行します。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

新しいビットレートでQoE オブジェクトを更新し、ビットレート変更イベントを実行します。

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Edge六]

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

>[!TAB Media Edge API]

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

QoE オブジェクトを更新し、イベントを実行します。

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB Chromecast]

QoS オブジェクトを新しいビットレートで更新し、ビットレート変更イベントを実行します。

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  4500,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB Roku 2.x]

QoS オブジェクトを新しいビットレートで更新し、ビットレート変更イベントを実行します。

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(4500.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
adb.mediaTrackEvent(adb.MEDIA_BITRATE_CHANGE)
```

>[!TAB Media Collection API]

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

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
