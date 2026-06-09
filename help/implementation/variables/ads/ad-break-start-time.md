---
title: 広告休憩の開始時間
description: コンテンツ内の広告ブレークの開始時間（オフセット）を秒単位で設定します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 6%

---


# 広告休憩の開始時間

>[!BEGINSHADEBOX]

*このページでは、**Ad Break Start Time**変数のデータ収集について説明します。 対応するレポートディメンションについては、[ ポッドの位置](/help/reporting/dimensions/pod-position.md)を参照してください。*

>[!ENDSHADEBOX]

広告枠の開始時間変数は、コンテンツ内の広告枠のオフセットです（秒単位）。 プリロールの場合、値は`0`です。ミッドロールの場合、値はブレークが始まる再生ヘッドの位置です。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.ad.podSecond` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.ad.podSecond` |
| **必須** | はい |
| **様が**&#x200B;様と共に送信されました | [広告ブレーク開始](/help/implementation/events/ads/ad-break-start.md)、広告クローズ |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.advertisingPodDetails`内に`offset`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "mid-roll-1",
        index: 2,
        offset: 90
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

3番目の引数として開始時間を秒単位で`createAdBreakObject`に渡します。

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

3番目の引数として開始時間を秒単位で`createAdBreakObject`に渡します。

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Edge六]

`media.adBreakStart`の`sendMediaEvent`を呼び出す場合、`xdm.mediaCollection.advertisingPodDetails`内に`offset`を設定します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "mid-roll-1",
                "index": 2,
                "offset": 90
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.advertisingPodDetails`内の`offset`で[adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) エンドポイントを呼び出します。

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "index": 2,
          "offset": 90
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

3番目の引数として開始時間を`ADB.Media.createAdBreakObject`に渡します。

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

3番目の引数として開始時間を秒単位で`ADBMobile.media.createAdBreakObject`に渡します。

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

2番目の引数として開始時間を秒単位で`adb_media_init_adbreakinfo`に渡します。 Roku パラメーターの順序に注意してください：`name, startTime, position`。

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("mid-roll-1", 90.0, 2)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB Media Collection API]

`adBreakStart` POST リクエストの`params` オブジェクトに`media.ad.podSecond`を含めます：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podSecond": 90
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
