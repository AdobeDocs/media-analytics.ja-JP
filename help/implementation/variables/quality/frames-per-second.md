---
title: フレーム/秒
description: QoE オブジェクトの現在のフレーム レートを設定して、バックエンドに品質レポート用のフレーム レート コンテキストを設定します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 7%

---


# フレーム/秒

1秒あたりのフレーム数は、ストリームの現在のフレームレートです。 QoE オブジェクト上でビットレートとドロップしたフレームと一緒に設定すると、バックエンドに各再生セッションの完全な品質コンテキストが表示されます。 Adobe Analyticsでは、フレームレートのレポート変数は自動作成されません。レポートとして表示する場合は、カスタム処理ルールを作成します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | なし（Adobe Analyticsでは、フレームレート用に予約されたコンテキストデータキーが割り当てられません） |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager特性** | 該当なし |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | 品質イベント （[&#x200B; ビットレート変更](/help/implementation/events/playback/bitrate-change.md)、[&#x200B; バッファー開始](/help/implementation/events/playback/buffer-start.md)、[&#x200B; エラー](/help/implementation/events/error.md)）、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.qoeDataDetails`内に`framesPerSecond`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        framesPerSecond: 24
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

フレームレートを3番目の引数（`fps`）として`createQoEObject`に渡します。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

フレームレートを3番目の引数（`fps`）として`createQoEObject`に渡します。

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Edge六]

`sendMediaEvent`の呼び出し時に`xdm.mediaCollection.qoeDataDetails`内に`framesPerSecond`を設定：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "framesPerSecond": 24
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.qoeDataDetails`内の`framesPerSecond`で[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) エンドポイントを呼び出します：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "framesPerSecond": 24
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

フレームレートを3番目の引数として`ADB.Media.createQoEObject`に渡します。

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

フレームレートを3番目の引数（`fps`）として`ADBMobile.media.createQoSObject`に渡し、トラッカーを更新します。

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

フレームレートを3番目の引数（`fps`）として`adb_media_init_qosinfo`に渡し、`mediaUpdateQoS`でトラッカーを更新します。

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB Media Collection API]

`params` オブジェクトに`media.qoe.framesPerSecond`を含めます：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.framesPerSecond": 24
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
