---
title: ポッド位置での広告
description: 親の広告ブレーク内の広告のインデックス位置を設定します。 最初の広告のインデックスは0です。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# ポッド位置での広告

>[!BEGINSHADEBOX]

*このページでは、ポッドの位置&#x200B;**変数の**&#x200B;広告のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; ポッド位置の広告](/help/reporting/dimensions/ad-in-pod-position.md)を参照してください。*

>[!ENDSHADEBOX]

ポッドの位置変数の広告は、親の広告ブレーク内の広告のインデックス付きゼロ位置です。 ポッドの最初の広告にはインデックス `0`が付いており、2番目の広告にはインデックス `1`が付いています。 ディメンションを使用して、広告枠の中の位置ごとにエンゲージメントと完了率を比較します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.ad.podPosition` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.advertisingDetails.podPosition`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.ad.podPosition` |
| **必須** | はい |
| **様が**&#x200B;様と共に送信されました | [広告の開始](/help/implementation/events/ads/ad-start.md)、広告の終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.advertisingDetails`内に`podPosition`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

位置を3番目の引数として`createAdObject`に渡します。

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

位置を3番目の引数として`createAdObject`に渡します。

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0L,
                                    15.0)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Edge六]

`media.adStart`の`sendMediaEvent`を呼び出す場合、`xdm.mediaCollection.advertisingDetails`内に`podPosition`を設定します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "podPosition": 0,
                "length": 15,
                "playerName": "Roku Player"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.advertisingDetails`内の`podPosition`で[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) エンドポイントを呼び出します：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
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

3番目の引数として位置を`ADB.Media.createAdObject`に渡します。

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",
  "ad-2125",
  0,
  15
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

3番目の引数として位置を`ADBMobile.media.createAdObject`に渡します。

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",
  "ad-2125",
  1,
  30
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

位置を3番目の引数として`adb_media_init_adinfo`に渡します。 ポッド内の広告位置は1 ベースです。

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)  ' name, id, position, length

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB Media Collection API]

`params` オブジェクトに`media.ad.podPosition`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.podPosition": 0
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
