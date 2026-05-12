---
title: 広告ブレーク名
description: 親の広告枠のわかりやすい名前を設定します。
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 12%

---


# 広告ブレーク名

>[!BEGINSHADEBOX]

*このページでは、**Ad break name**変数のデータ収集について説明します。 対応するレポートディメンションについては、[Pod name](/help/reporting/dimensions/pod-name.md)を参照してください。*

>[!ENDSHADEBOX]

広告ブレーク名変数は、広告ブレークのわかりやすい名前です（例：`"pre-roll"`、`"mid-roll-1"`、`"post-roll"`）。 値は、個々の広告ではなく、広告分割オブジェクトに設定されます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.ad.podFriendlyName` |
| **XDM コレクションフィールド** | [`mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **必須** | はい（モバイル SDK）、いいえ（Edge、Media Collection API） |
| **様が**&#x200B;様と共に送信されました | 開始、終了 |

## Web SDK

`media.adBreakStart`の[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を呼び出す場合、`mediaCollection.advertisingPodDetails`内に`friendlyName`を設定します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## モバイル SDK

広告ブレーク名を最初の（`name`）引数として`createAdBreakObject`に渡し、広告ブレーク開始イベントを広告ブレーク開始イベントの前に追跡します。

**iOS （Swift）**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android （Kotlin）**

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku （BrightScript）

`media.adBreakStart`の`sendMediaEvent`を呼び出す場合、`mediaCollection.advertisingPodDetails`内に`friendlyName`を設定します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.advertisingPodDetails`内の`friendlyName`で[adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) エンドポイントを呼び出します。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "friendlyName": "pre-roll",
          "index": 1,
          "offset": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

広告ブレーク名を最初の引数として`ADB.Media.createAdBreakObject`に渡します：

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## メディアコレクション API

`adBreakStart` POST リクエストの`params` オブジェクトに`media.ad.podFriendlyName`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
