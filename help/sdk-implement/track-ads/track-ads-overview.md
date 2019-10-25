---
seo-title: 概要
title: 概要
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# 概要{#overview}

>[!IMPORTANT]
>
>2.x SDKを使用した導入に関するガイダンスを以下に示します。 If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

広告再生には、広告ブレーク、広告開始、広告完了、広告スキップの追跡が含まれます。メディアプレイヤーのAPIを使用して、主要なプレーヤーイベントを識別し、必要な広告変数とオプションの広告変数を設定します。 詳しくは、メタデータの詳細なリストを参照してください。広告パラ [メーター。](/help/metrics-and-metadata/ad-parameters.md)

## プレーヤーイベント {#player-events}


### 広告の時間開始時

>[!NOTE]
>プリロールを含む

* 広告ブレークの `adBreak` オブジェクトインスタンスを作成します。例：`adBreakObject`。

* Call `trackEvent` for the ad break start with your `adBreakObject`.

### すべての広告アセットの開始時

* 広告アセットの広告オブジェクトインスタンスを作成します。例：`adObject`。
* Populate the ad metadata, `adCustomMetadata`.
* 広告開始の `trackEvent` を呼び出します。

### すべての広告の完了時

* 広告完了の `trackEvent` を呼び出します。

### 広告スキップ時

* 広告スキップの `trackEvent` を呼び出します。

### 広告ブレークの完了時

* ブレーク完了の `trackEvent` を呼び出します。

## 広告トラッキングの実装 {#implement-ad-tracking}

### 広告トラッキング定数

| 定数名 | 説明   |
|---|---|
| `AdBreakStart` | 追跡する AdBreak Start イベントの定数 |
| `AdBreakComplete` | 追跡する AdBreak Complete イベントの定数 |
| `AdStart` | 追跡する Ad Start イベントの定数 |
| `AdComplete` | 追跡する Ad Complete イベントの定数 |
| `AdSkip` | 追跡する Ad Skip イベントの定数 |

### 導入手順

1. プリロールを含め、いつ広告ブレークの境界が開始するかを識別し、広告ブレーク情報を使用して `AdBreakObject` を作成します。

   `AdBreakObject` 参照：

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | プリロール、ミッドロール、ポストロールなど、広告ブレークの名前 | ○ |
   | `position` | コンテンツ内の広告ブレークの位置番号（1 から始まる）。 | ○ |
   | `startTime` | 広告ブレーク開始時の再生ヘッド値 | ○ |

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break.

1. いつ広告が開始するかを識別し、広告情報を使用して `AdObject` インスタンスを作成します。

   `AdObject` 参照：

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | 広告のわかりやすい名前。 | ○ |
   | `adId` | 広告の一意の識別子。 | ○ |
   | `position` | 広告ブレーク内の広告の位置番号（1 から始まる）。 | ○ |
   | `length` | 広告の長さ | ○ |

1. オプションで、コンテキストデータ変数を使用して標準または広告メタデータをトラッキングセッションにアタッチします。

   * **標準広告メタデータ** - 標準広告メタデータの場合、ご利用のプラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。
   * **カスタムの広告メタデータ** - カスタムのメタデータの場合は、カスタムデータ変数の変数オブジェクトを作成し、現在の広告のデータを設定します。

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   カスタムメタデータ変数（または空のオブジェクト）への参照を、イベント呼び出しの 3 番目のパラメーターとして追加します。

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

1. ユーザーが広告のスキップを選択したので広告再生が完了しなかった場合は、`AdSkip` イベントを追跡します。
1. 同じ `AdBreak` にその他の広告がある場合、手順 3 ～ 7 を繰り返します。
1. When the ad break is complete, use the `AdBreakComplete` event to track it.

>[!IMPORTANT]
>
>広告の再生中は、コンテンツプレーヤーの再生ヘッド(`l:event:playhead`)を増やさないようにし`s:asset:type=ad`ます。 この場合、コンテンツ滞在時間指標に悪影響が及びます。

以下のサンプルコードは、HTML5メディアプレイヤー用のJavaScript 2.x SDKを使用しています。

```js
/* Call on ad break start */ 
 
if (e.type == "ad break start") { 
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500); 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject); 
}; 
 
/* Call on ad start */ 
if (e.type == "ad start") { 
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30); 
    /* Set custom context data */ 
    var adCustomMetadata = { 
        affiliate:"Sample affiliate", 
        campaign:"Sample ad campaign", 
        creative:"Sample creative" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata); 
}; 
 
/* Call on ad complete */ 
if (e.type == "ad complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
}; 
 
/* Call on ad skip */ 
if (e.type == "ad skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
}; 
     
/* Call on ad break complete */ 
if (e.type == "ad break complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
}; 
```

