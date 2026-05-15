---
title: キャンペーン ID
description: 各広告のキャンペーン IDを設定し、キャンペーンごとにエンゲージメントを集約できるようにします。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 15%

---


# キャンペーン ID

>[!BEGINSHADEBOX]

*このページでは、**Campaign ID**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[&#x200B; キャンペーン ID](/help/reporting/dimensions/campaign-id.md)を参照してください。*

>[!ENDSHADEBOX]

キャンペーン ID変数は、クリエイティブが属する広告キャンペーンを識別します。 任意の文字列値（通常は、広告サーバープラットフォームのキャンペーン ID）を使用できます。 この変数を使用して、キャンペーンを共有する複数のクリエイター間でエンゲージメントをロールアップします。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.ad.campaign` |
| **XDM コレクションフィールド** | [`mediaCollection.advertisingDetails.campaignID`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.ad.campaign` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [広告の開始](/help/implementation/events/ads/ad-start.md)、広告の終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.advertisingDetails`内に`campaignID`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        campaignID: "fall-2024"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## モバイル SDK

キャンペーン IDをHashMap引数のメタデータキーとして`trackEvent(AdStart)`に渡します。 `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.を使用します。

**iOS （Swift）**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android （Kotlin）**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku （BrightScript）

`media.adStart`の`sendMediaEvent`を呼び出す場合、`mediaCollection.advertisingDetails`内に`campaignID`を設定します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "campaignID": "fall-2024"
            },
            "playhead": 0
        }
    }
})
```

## Media Edge API

`mediaCollection.advertisingDetails`内の`campaignID`で[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) エンドポイントを呼び出します：

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
          "podPosition": 0,
          "campaignID": "fall-2024"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## メディア SDK

`ADB.Media.AdMetadataKeys.CampaignId`を使用して`contextData` オブジェクトにキャンペーン IDを渡します：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CampaignId] = "fall-2024";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## メディアコレクション API

`params` オブジェクトに`media.ad.campaignId`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.campaignId": "fall-2024"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
