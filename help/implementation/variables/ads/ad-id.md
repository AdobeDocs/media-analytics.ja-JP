---
title: 広告 ID
description: 広告を一意に識別：
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 10%

---


# 広告 ID

>[!BEGINSHADEBOX]

*このページでは、**Ad ID**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[Ad](/help/reporting/dimensions/ad.md)を参照してください。*

>[!ENDSHADEBOX]

広告ID変数は、各広告を一意に識別します。 プレーヤーが追跡するすべての広告に必要です。 `media.adStart` イベントごとに設定します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.ad.name` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.advertisingDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.ad.name` |
| **必須** | はい |
| **様が**&#x200B;様と共に送信されました | [広告の開始](/help/implementation/events/ads/ad-start.md)、広告の終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

`media.adStart`の[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)を呼び出す場合、`xdm.mediaCollection.advertisingDetails`内に`name`を設定します：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        friendlyName: "Ford F-150",
        length: 15,
        playerName: "Freewheel",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

広告IDを`adId`引数として`createAdObject`に渡します。 最初の引数（`name`）はフレンドリ名、2番目の引数はIDです。

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

広告IDを`adId`引数として`createAdObject`に渡します。 最初の引数（`name`）はフレンドリ名、2番目の引数はIDです。

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0L,
                                    15.0)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku]

`media.adStart`の`sendMediaEvent`を呼び出す場合、`xdm.mediaCollection.advertisingDetails`内に`name`を設定します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "friendlyName": "Ford F-150",
                "length": 15,
                "playerName": "Roku Player",
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.advertisingDetails`内の`name`で[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) エンドポイントを呼び出します：

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

広告IDを2番目の引数として`ADB.Media.createAdObject`に渡します：

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",   // name (friendly name)
  "ad-2125",      // ad ID
  0,              // position in pod
  15              // length (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

広告IDを2番目の引数として`ADBMobile.media.createAdObject`に渡します：

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",
  "ad-2125",
  1,
  30
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Media Collection API]

`adStart` POST リクエストの`params` オブジェクトに`media.ad.id`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "ad-2125"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
