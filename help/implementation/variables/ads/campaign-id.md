---
title: キャンペーン ID
description: 各広告のキャンペーン IDを設定し、キャンペーンごとにエンゲージメントを集約できるようにします。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 10%

---


# キャンペーン ID

>[!BEGINSHADEBOX]

*このページでは、**Campaign ID**変数のデータ収集について説明します。 対応するレポートディメンションについては、[ キャンペーン ID](/help/reporting/dimensions/campaign-id.md)を参照してください。*

>[!ENDSHADEBOX]

キャンペーン ID変数は、クリエイティブが属する広告キャンペーンを識別します。 任意の文字列値（通常は、広告サーバープラットフォームのキャンペーン ID）を使用できます。 この変数を使用して、キャンペーンを共有する複数のクリエイター間でエンゲージメントをロールアップします。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.ad.campaign` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.ad.campaign` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [広告の開始](/help/implementation/events/ads/ad-start.md)、広告の終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.advertisingDetails`内に`campaignID`を設定：

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

>[!TAB iOS]

キャンペーン IDをHashMap引数のメタデータキーとして`trackEvent(AdStart)`に渡します。 `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.を使用します。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

キャンペーン IDをHashMap引数のメタデータキーとして`trackEvent(AdStart)`に渡します。 `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.を使用します。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku]

`media.adStart`の`sendMediaEvent`を呼び出す場合、`xdm.mediaCollection.advertisingDetails`内に`campaignID`を設定します：

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

>[!TAB Media Edge API]

`xdm.mediaCollection.advertisingDetails`内の`campaignID`で[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) エンドポイントを呼び出します：

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

>[!ENDTABS]

## 従来の実装タイプ （Analyticsのみ）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

`ADB.Media.AdMetadataKeys.CampaignId`を使用して`contextData` オブジェクトにキャンペーン IDを渡します：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CampaignId] = "fall-2024";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

標準広告メタデータオブジェクトの`ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID`を使用してキャンペーン IDを設定します。

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Media Collection API]

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

完全なリクエスト構造については、[Media Collection API イベントのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
