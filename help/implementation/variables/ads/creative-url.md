---
title: クリエイティブ URL
description: 各広告の広告クリエイティブのURLを設定します。
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 16%

---


# クリエイティブ URL

>[!BEGINSHADEBOX]

*このページでは、**Creative URL**変数のデータ収集について説明します。 対応するレポートディメンションについては、[Creative URL](/help/reporting/dimensions/creative-url.md)を参照してください。*

>[!ENDSHADEBOX]

クリエイティブ URL変数は、広告クリエイティブのURLです。 変数を使用すると、URL自体が分析に役立つ場合（CDN パスやクリエイティブバージョンの区別など）に、各クリエイティブのアセットの場所を追跡できます。

| プロパティ | 値 |
| --- | --- |
| **コンテキストデータ変数** | `a.media.ad.creativeURL` |
| **XDM コレクションフィールド** | [`mediaCollection.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特性** | `c_contextdata.a.media.ad.creativeURL` |
| **必須** | いいえ |
| **様が**&#x200B;様と共に送信されました | [広告の開始](/help/implementation/events/ads/ad-start.md)、広告の終了 |

## Web SDK

[`sendEvent`](https://experienceleague.adobe.com/ja/docs/experience-platform/collection/js/commands/sendevent/overview)の呼び出し時に`mediaCollection.advertisingDetails`内に`creativeURL`を設定：

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

## モバイル SDK

クリエイティブ URLをHashMap引数のメタデータキーとして`trackEvent(AdStart)`に渡します。 `MediaConstants.AdMetadataKeys.CREATIVE_URL`.を使用します。

**iOS （Swift）**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android （Kotlin）**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku （BrightScript）

`media.adStart`の`sendMediaEvent`を呼び出す場合、`mediaCollection.advertisingDetails`内に`creativeURL`を設定します：

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

## Media Edge API

`mediaCollection.advertisingDetails`内の`creativeURL`で[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) エンドポイントを呼び出します：

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

## メディア SDK

`ADB.Media.AdMetadataKeys.CreativeUrl`を使用して、`contextData` オブジェクト内のクリエイティブ URLを渡します：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeUrl] = "https://cdn.example.com/ads/creative-987.mp4";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## メディアコレクション API

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

完全なリクエスト構造については、[Media Collection API イベントのリファレンス ](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)を参照してください。
