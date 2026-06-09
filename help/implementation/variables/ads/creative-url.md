---
title: クリエイティブ URL
description: 各広告の広告クリエイティブのURLを設定します。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 10%

---


# クリエイティブ URL

>[!BEGINSHADEBOX]

*このページでは、**Creative URL**&#x200B;変数のデータ収集について説明します。 対応するレポートディメンションについては、[Creative URL](/help/reporting/dimensions/creative-url.md)を参照してください。*

>[!ENDSHADEBOX]

クリエイティブ URL変数は、広告クリエイティブのURLです。 変数を使用すると、URL自体が分析に役立つ場合（CDN パスやクリエイティブバージョンの区別など）に、各クリエイティブのアセットの場所を追跡できます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.ad.creativeURL` |
| **XDM コレクションフィールド** | [`xdm.mediaCollection.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.ad.creativeURL` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [広告の開始](/help/implementation/events/ads/ad-start.md)、広告の終了 |

## 推奨される実装タイプ

>[!BEGINTABS]

>[!TAB Web SDK]

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`xdm.mediaCollection.advertisingDetails`内に`creativeURL`を設定：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        creativeURL: "https://cdn.example.com/ads/creative-987.mp4"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

クリエイティブ URLをHashMap引数のメタデータキーとして`trackEvent(AdStart)`に渡します。 `MediaConstants.AdMetadataKeys.CREATIVE_URL`.を使用します。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

クリエイティブ URLをHashMap引数のメタデータキーとして`trackEvent(AdStart)`に渡します。 `MediaConstants.AdMetadataKeys.CREATIVE_URL`.を使用します。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Edge六]

`media.adStart`の`sendMediaEvent`を呼び出す場合、`xdm.mediaCollection.advertisingDetails`内に`creativeURL`を設定します：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

`xdm.mediaCollection.advertisingDetails`内の`creativeURL`で[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) エンドポイントを呼び出します：

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
          "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
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

`ADB.Media.AdMetadataKeys.CreativeUrl`を使用して、`contextData` オブジェクト内のクリエイティブ URLを渡します：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeUrl] = "https://cdn.example.com/ads/creative-987.mp4";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

標準の広告メタデータオブジェクトで`ADBMobile.media.AdMetadataKeys.CREATIVE_URL`を使用してクリエイティブ URLを設定します。

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

標準の広告メタデータオブジェクトで`MEDIA_AdMetadataKeyCREATIVE_URL`を使用してクリエイティブ URLを設定します。

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyCREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB Media Collection API]

`params` オブジェクトに`media.ad.creativeURL`を含めます：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
  }
}
```

完全なリクエスト構造については、[Media Collection API イベントのリファレンス &#x200B;](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。

>[!ENDTABS]
