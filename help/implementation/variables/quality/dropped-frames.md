---
title: ドロップしたフレーム
description: バックエンドがフレームドロップの品質を報告できるように、QoE オブジェクトにドロップされたフレームの実行回数を設定します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 5%

---


# ドロップしたフレーム

>[!BEGINSHADEBOX]

*このページでは、**削除されたフレーム**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションと指標については、[削除されたフレーム &#x200B;](/help/reporting/dimensions/dropped-frames.md)を参照してください。*

>[!ENDSHADEBOX]

ドロップされたフレーム変数は、セッション中にプレイヤーがドロップしたフレームのランニングカウントです。 QoE オブジェクトに設定し、プレイヤーが新しいドロップを報告するたびに値を更新します。 バックエンドは、セッションのクローズ時に最新の値をレポートします。

>[!NOTE]
>
>セッション全体のドロップされたフレームの&#x200B;**累計**&#x200B;をその時点まで常に渡します。間隔ごとの差分は渡しません。 更新の間に値を`0`にリセットすると、バックエンドは最終値として`0`を受け取り、実際に以前にドロップしたものに関係なく、セッションのドロップ済みフレームがゼロであるとレポートします。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.qoe.droppedFrameCount` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.qoe.droppedFrameCount` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | 品質イベント （[&#x200B; ビットレート変更](/help/implementation/events/playback/bitrate-change.md)、[&#x200B; バッファー開始](/help/implementation/events/playback/buffer-start.md)、[&#x200B; エラー](/help/implementation/events/error.md)）、セッション終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.qoeDataDetails`内に`droppedFrames`を設定：

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

>[!TAB iOS]

4番目の引数としてドロップしたフレームを`createQoEObject`に渡します。 品質イベントが発生する前に、トラッカーを更新します。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

4番目の引数としてドロップしたフレームを`createQoEObject`に渡します。 品質イベントが発生する前に、トラッカーを更新します。

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

`sendMediaEvent`の呼び出し時に`xdm.mediaCollection.qoeDataDetails`内に`droppedFrames`を設定：

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

>[!TAB Media Edge API]

`xdm.mediaCollection.qoeDataDetails`内の`droppedFrames`で[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) エンドポイントを呼び出します：

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

ドロップしたフレームを4番目の引数として`ADB.Media.createQoEObject`に渡します。

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

累積ドロップされたフレーム数を4番目の引数として`ADBMobile.media.createQoSObject`に渡し、トラッカーを更新します。

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames (cumulative total)
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Media Collection API]

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

>[!ENDTABS]
