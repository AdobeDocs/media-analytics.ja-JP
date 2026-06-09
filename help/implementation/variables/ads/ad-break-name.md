---
title: 広告ブレーク名
description: 親の広告枠のわかりやすい名前を設定します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 6%

---


# 広告ブレーク名

>[!BEGINSHADEBOX]

*このページでは、**Ad break name**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[Pod name](/help/reporting/dimensions/pod-name.md)を参照してください。*

>[!ENDSHADEBOX]

広告ブレーク名変数は、広告ブレークのわかりやすい名前です（例：`"pre-roll"`、`"mid-roll-1"`、`"post-roll"`）。 値は、個々の広告ではなく、広告分割オブジェクトに設定されます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.ad.podFriendlyName` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.ad.podFriendlyName` |
| **必須** | はい（モバイル SDK）、いいえ（Edge、Media Collection API） |
| **様が**&#x200B;様と共に送信されました | [広告ブレーク開始](/help/implementation/events/ads/ad-break-start.md)、広告クローズ |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

`media.adBreakStart`の[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を呼び出す場合、`xdm.mediaCollection.advertisingPodDetails`内に`friendlyName`を設定します：

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

>[!TAB iOS]

広告ブレーク名を最初の（`name`）引数として`createAdBreakObject`に渡し、広告ブレーク開始イベントを広告ブレーク開始イベントの前に追跡します。

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

広告ブレーク名を最初の（`name`）引数として`createAdBreakObject`に渡し、広告ブレーク開始イベントを広告ブレーク開始イベントの前に追跡します。

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Edge六]

`media.adBreakStart`の`sendMediaEvent`を呼び出す場合、`xdm.mediaCollection.advertisingPodDetails`内に`friendlyName`を設定します：

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

>[!TAB Media Edge API]

`xdm.mediaCollection.advertisingPodDetails`内の`friendlyName`で[adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) エンドポイントを呼び出します。

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

広告ブレーク名を最初の引数として`ADB.Media.createAdBreakObject`に渡します：

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

広告ブレーク名を最初の引数として`ADBMobile.media.createAdBreakObject`に渡します：

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",
  1,
  0
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

広告ブレーク名を最初の引数として`adb_media_init_adbreakinfo`に渡します。 Roku パラメーターの順序に注意してください：`name, startTime, position`。

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("pre-roll", 0.0, 1)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB Media Collection API]

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

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
