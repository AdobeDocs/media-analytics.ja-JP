---
title: 広告プレーヤー名
description: 広告をレンダリングするプレーヤーの名前を設定します。 広告プレーヤーは、メインコンテンツプレーヤーとは異なる場合があります。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 6%

---


# 広告プレーヤー名

>[!BEGINSHADEBOX]

*このページでは、**広告プレーヤー名**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[Ad player name](/help/reporting/dimensions/ad-player-name.md)を参照してください。*

>[!ENDSHADEBOX]

広告プレーヤー名変数は、各広告をレンダリングしたプレーヤーを識別します（例：`"Freewheel"`、`"Google IMA"`）。 広告プレーヤは、サーバサイドの広告挿入サービスによって広告がステッチされる場合、メインコンテンツプレーヤとは異なっていてもよい。 この変数は、広告配信スタック全体の品質と完了率を比較するために使用します。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.ad.playerName` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.ad.playerName` |
| **必須** | はい |
| **様が**&#x200B;様と共に送信されました | [広告の開始](/help/implementation/events/ads/ad-start.md)、広告の終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.advertisingDetails`内に`playerName`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        playerName: "Freewheel"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

メタデータ HashMap引数の`MediaConstants.AdMetadataKeys.AD_PLAYER` キーとして広告プレーヤー名を`trackEvent(AdStart)`に渡します。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

メタデータ HashMap引数の`MediaConstants.AdMetadataKeys.AD_PLAYER` キーとして広告プレーヤー名を`trackEvent(AdStart)`に渡します。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Edge六]

`media.adStart`の`sendMediaEvent`を呼び出す場合、`xdm.mediaCollection.advertisingDetails`内に`playerName`を設定します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "playerName": "Freewheel",
                "length": 15,
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.advertisingDetails`内の`playerName`で[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) エンドポイントを呼び出します：

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

`ADB.Media.AdMetadataKeys.AdPlayer`を使用して、`contextData` オブジェクトに広告プレーヤー名を渡します：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

広告開始イベントをトラッキングする際に、コンテキストメタデータオブジェクトに広告プレーヤー名を渡します。

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var metadata = { "a.media.ad.playerName": "Chromecast Player" };
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, metadata);
```

>[!TAB Roku 2.x]

広告開始イベントをトラッキングする際に、コンテキストデータオブジェクトに広告プレーヤー名を渡します。

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

contextData = { "a.media.ad.playerName": "Roku Player" }
adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo, contextData)
```

>[!TAB Media Collection API]

`adStart` POST リクエストの`params` オブジェクトに`media.ad.playerName`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.playerName": "Freewheel"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
