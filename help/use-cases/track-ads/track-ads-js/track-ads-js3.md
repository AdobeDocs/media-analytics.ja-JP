---
title: JavaScript 3.x を使用して広告をトラッキングする方法
description: メディア SDK を使用して、ブラウザー（JS）アプリケーションに広告トラッキングを実装します。
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/j8xAr1QwslwoGu5IKvW14wFjyCSMMIIerA1t-JECNcQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 406
ht-degree: 88%

---

# JavaScript 3.x を使用した広告の追跡{#track-ads-on-javascript}

以下の手順は、SDK 3.x を使用した実装についてのガイダンスです。

>[!IMPORTANT]
>
>以前のバージョンの SDK を実装している場合は、[SDK のダウンロード](/help/getting-started/download-sdks.md)から開発者ガイドをダウンロードできます。

## 広告トラッキングの定数

| 定数名 | 説明   |
|---|---|
| `AdBreakStart` | 追跡する AdBreak Start イベントの定数 |
| `AdBreakComplete` | 追跡する AdBreak Complete イベントの定数 |
| `AdStart` | 追跡する Ad Start イベントの定数 |
| `AdComplete` | 追跡する Ad Complete イベントの定数 |
| `AdSkip` | 追跡する Ad Skip イベントの定数 |

## 実装手順

1. プリロールを含め、いつ広告ブレークの境界が開始するかを識別し、広告ブレーク情報を使用して `AdBreakObject` を作成します。

   `AdBreakObject` リファレンス：

   | 変数名 | タイプ | 説明 |
   | --- | --- | --- |
   | `name` | string | 広告ブレーク名（プレロール、ミッドロール、ポストロール）を示す空白以外の文字列。 |
   | `position` | number | 広告ブレークの位置番号（1 から始まる） |
   | `startTime` | number | 広告ブレーク開始時の再生ヘッド値 |

   広告ブレークオブジェクトの作成：

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. `MediaHeartbeat` インスタンスの `AdBreakStart` で `trackEvent()` を呼び出し、広告ブレークの追跡を開始します。

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. いつ広告が開始するかを識別し、広告情報を使用して `AdObject` インスタンスを作成します。

   `AdObject` リファレンス：

   | 変数名 | タイプ | 説明 |
   | --- | --- | --- |
   | `name` | string | 広告名を示す空白以外の文字列。 |
   | `adId` | string | 広告識別子を示す空白以外の文字列。 |
   | `position` | number | 広告ブレーク内の広告の位置を示す番号（1 から始まります）。 |
   | `length` | number | 広告の長さを示す正の数。 |

   広告オブジェクトの作成：

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. （オプション）コンテキストデータ変数を使用して、標準および/または広告メタデータをメディアトラッキングセッションに添付します。

   * [JavaScript での標準広告メタデータの実装](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **カスタムの広告メタデータ** - カスタムのメタデータの場合は、カスタムデータ変数の変数オブジェクトを作成し、現在の広告のデータを設定します。

     ```js
     /* Set context data */
     // Standard metadata keys provided by adobe.
     adMetadata[ADB.Media.AdMetadataKeys]  ="Sample Advertiser";
     adMetadata[ADB.Media.AdMetadataKeys] = "Sample Campaign";
     
     // Custom metadata keys
     adMetadata["affiliate"] = "Sample affiliate";
     adMetadata["campaign"] = "Sample ad campaign";
     adMetadata["creative"] = "Sample creative";
     ```

1. `MediaHeartbeat` インスタンスの `AdStart` イベントで `trackEvent()` を呼び出し、広告再生の追跡を開始します。

   カスタムメタデータ変数（または空のオブジェクト）への参照を、イベント呼び出しの 3 番目のパラメーターとして含めます。

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. 広告の再生が広告の終わりに到達したら、`AdComplete` イベントで `trackEvent()` を呼び出します。

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. ユーザーが広告のスキップを選択したので広告再生が完了しなかった場合は、`AdSkip` イベントを追跡します。

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. 同じ `AdBreak` にその他の広告がある場合、手順 3 ～ 7 を繰り返します。
1. 広告ブレークが完了したら、`AdBreakComplete` イベントを使用して追跡します。

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

詳しくは、追跡シナリオの[プリロール広告のある VOD 再生](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)を参照してください。

## きめ細かい広告トラッキング

デフォルトの広告ping間隔は`10 seconds`です。

詳細な広告トラッキングを設定して、`1 second`広告トラッキングを有効にすることができます。

>[!IMPORTANT]
>
>この情報は、トラッキングセッションを開始する際に提供する必要があります。



**構文**

```javascript
ADB.Media.MediaObjectKey = {
   GranularAdTracking: "media.granularadtracking"
   }
```

**例**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

// Enable granular ad tracking
mediaObject[ADB.Media.MediaObjectKey.GranularAdTracking] = true;

tracker.trackSessionStart(mediaObject);
```
