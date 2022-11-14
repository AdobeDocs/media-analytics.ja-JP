---
title: Chromecast で広告をトラッキングする方法
description: メディア SDK を使用して、Chromecast アプリケーションに広告トラッキングを実装します。
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
exl-id: 57465c42-b349-439d-b8d7-083b299a8c83
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 100%

---

# Chromecast での広告の追跡{#track-ads-on-chromecast}

以下の手順は、SDK 2.x を使用した実装についてのガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

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

   広告ブレークオブジェクトの作成：[createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName);
   ```

1. `MediaHeartbeat` インスタンスの `AdBreakStart` で `trackEvent()` を呼び出し、広告ブレークの追跡を開始します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. いつ広告アセットが開始するかを識別し、広告情報を使用して `AdObject` インスタンスを作成します。

   広告オブジェクトの作成：[createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH);
   ```

1. オプションで、コンテキストデータ変数を使用して標準または広告メタデータをメディアトラッキングセッションにアタッチします。

   * **標準広告メタデータ** - 標準広告メタデータの場合、ご利用のプラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。
   * **カスタムの広告メタデータ** - カスタムのメタデータの場合は、カスタムデータ変数の変数オブジェクトを作成し、現在の広告アセットのデータを設定します。

1. `AdStart` イベントで `trackEvent()` を呼び出し、広告再生の追跡を開始します。

   カスタムメタデータ変数（または空のオブジェクト）への参照を、イベント呼び出しの 3 番目のパラメーターとして追加します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. 広告アセットの再生が広告の終わりに到達したら、`AdComplete` イベントで `trackEvent()` を呼び出します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
   ```

1. 同じ `AdBreak` にその他の広告がある場合、手順 3 ～ 6 を繰り返します。
1. 広告ブレークが完了したら、`AdBreakComplete` イベントを使用して追跡します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

詳しくは、追跡シナリオの[プリロール広告のある VOD 再生](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)を参照してください。
