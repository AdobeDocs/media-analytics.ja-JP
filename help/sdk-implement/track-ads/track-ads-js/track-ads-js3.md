---
title: JavaScript 3.xを使用した広告の追跡方法を説明します。
description: メディア SDK を使用して、ブラウザー（JS）アプリケーションに広告トラッキングを実装します。
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 97%

---

# JavaScript 3.x を使用した広告の追跡{#track-ads-on-javascript}

>[!IMPORTANT]
>
>以下の手順は、SDK 3.x を使用した実装についてのガイダンスです。以前のバージョンの SDK を実装している場合は、[SDK のダウンロード](/help/sdk-implement/download-sdks.md)から開発者ガイドをダウンロードできます。

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
   | `position` | 数値 | 広告ブレークの位置番号（1 から始まる） |
   | `startTime` | 数値 | 広告ブレーク開始時の再生ヘッド値 |

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
   | `name` | 文字列 | 広告名を示す空白以外の文字列。 |
   | `adId` | 文字列 | 広告識別子を示す空白以外の文字列。 |
   | `position` | 数値 | 広告ブレーク内の広告の位置を示す番号（1 から始まります）。 |
   | `length` | 数値 | 広告の長さを示す正の数。 |

   広告オブジェクトの作成：

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. オプションで、コンテキストデータ変数を使用して標準または広告メタデータをメディアトラッキングセッションにアタッチします。

   * [JavaScript での標準広告メタデータの実装](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
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

詳しくは、追跡シナリオの[プリロール広告のある VOD 再生](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md)を参照してください。
