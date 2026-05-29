---
title: ビットレートの変更
description: 再生ビットレートが変更されたことを示します。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 7%

---


# ビットレートの変更

ビットレート変更イベントは、プレーヤーが新しい再生ビットレートを交渉したことを示します。 再生中にビットレートが変更されるたびに送信します。 新しいビットレート値をQoE データに含めて、バックエンドが[[!UICONTROL 平均ビットレート &#x200B;]](/help/reporting/metrics/average-bitrate.md)とビットレートごとのバケット ディメンションを計算できるようにします。

* **前提条件**: [&#x200B; セッション開始](../session/session-start.md)
* **関連する指標**: [[!UICONTROL &#x200B; ビットレートの変更]](/help/reporting/metrics/bitrate-changes.md)

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を`eventType: "media.bitrateChange"`で呼び出し、新しいビットレートを`qoeDataDetails`で呼び出します。

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

新しいビットレートでQoE オブジェクトを作成し、ビットレート変更イベントが発生する前にトラッカーを更新します。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

新しいビットレートでQoE オブジェクトを作成し、ビットレート変更イベントが発生する前にトラッカーを更新します。

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku]

`sendMediaEvent`を`eventType: "media.bitrateChange"`で呼び出し、新しいビットレートを`qoeDataDetails`で呼び出します：

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

`qoeDataDetails`の新しいビットレートで[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/) エンドポイントを呼び出します。

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bitrateChange?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

新しいビットレートでQoE オブジェクトを作成し、トラッカーを更新します。

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB Chromecast]

`getQoSObject` デリゲートから返されたQoS オブジェクトを更新し、イベントを追跡します。

```javascript
// Update QoS data via the delegate
this._qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // dropped frames
  24,    // fps
  0      // startup time
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB Media Collection API]

`qoeData`の新しいビットレートを使用して、[&#x200B; イベントエンドポイント &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)に`bitrateChange` POSTを送信します。

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "qoeData": {
    "media.qoe.bitrate": 3200
  }
}
```

>[!ENDTABS]
