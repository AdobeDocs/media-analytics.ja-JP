---
seo-title: 概要
title: 概要
uuid: 1607798b- c6ef-4d60-8e40- e958c345b09c
translation-type: tm+mt
source-git-commit: 56e8716ea37049b95a59a82144bbad0e882c16b4

---


# 概要{#overview}

>[!IMPORTANT]
>
>次の手順では、2. x SDKを使用した導入について説明します。If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

広告再生には、広告ブレーク、広告開始、広告完了、広告スキップの追跡が含まれます。メディアプレイヤーのAPIを使用して、主要プレーヤーイベントを識別し、必須およびオプションの広告変数を設定します。See the comprehensive list of metadata here: [Ad parameters.](../../metrics-and-metadata/ad-parameters.md)

## Player events {#player-events}


### 広告の時間開始時

>[!NOTE]
>プリロールのインクルード

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

## Implement ad tracking {#section_83E0F9406A7743E3B57405D4CDA66F68}

### 広告トラッキング定数

| 定数名 | 説明   |
|---|---|
| `AdBreakStart` | 追跡する AdBreak Start イベントの定数 |
| `AdBreakComplete` | 追跡する AdBreak Complete イベントの定数 |
| `AdStart` | 追跡する Ad Start イベントの定数 |
| `AdComplete` | 追跡する Ad Complete イベントの定数 |
| `AdSkip` | 追跡する Ad Skip イベントの定数 |

### 実装手順

1. プリロールを含め、いつ広告ブレークの境界が開始するかを識別し、広告ブレーク情報を使用して `AdBreakObject` を作成します。

   `AdBreakObject` 参照:

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | プリロール、ミッドロール、ポストロールなど、広告ブレークの名前 | ○ |
   | `position` | コンテンツ内の広告ブレークの位置番号（1 から始まる）。 | ○ |
   | `startTime` | 広告ブレーク開始時の再生ヘッド値 | ○ |

1. `trackEvent()` インスタンス `AdBreakStart` 内で `MediaHeartbeat` 呼び出して、広告の時間の追跡を開始します。

1. いつ広告が開始するかを識別し、広告情報を使用して `AdObject` インスタンスを作成します。

   `AdObject` 参照:

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | 広告のわかりやすい名前。 | ○ |
   | `adId` | 広告の一意の識別子。 | ○ |
   | `position` | 広告ブレーク内の広告の位置番号（1 から始まる）。 | ○ |
   | `length` | 広告の長さ | ○ |

1. オプションで、コンテキストデータ変数を使用して標準または広告メタデータをトラッキングセッションにアタッチします。

   * **標準広告メタデータ** - 標準広告メタデータの場合、ご利用のプラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。
   * **カスタムの広告メタデータ** - カスタムのメタデータの場合は、カスタムデータ変数の変数オブジェクトを作成し、現在の広告のデータを設定します。

1. `trackEvent()` インスタンス内の `AdStart` イベント `MediaHeartbeat` を呼び出して、広告再生の追跡を開始します。

   カスタムメタデータ変数（または空のオブジェクト）への参照を、イベント呼び出しの 3 番目のパラメーターとして追加します。

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

1. ユーザーが広告のスキップを選択したので広告再生が完了しなかった場合は、`AdSkip` イベントを追跡します。
1. 同じ `AdBreak` にその他の広告がある場合、手順 3 ～ 7 を繰り返します。
1. When the ad break is complete, use the `AdBreakComplete` event to track it.

>[!IMPORTANT]
>
>Make sure you do NOT increment the content player playhead (`l:event:playhead`) during ad playback (`s:asset:type=ad`). その場合、コンテンツ滞在時間指標は悪影響を受けます。

以下のサンプルコードは、HTML5メディアプレイヤー用JavaScript2. x SDKを使用しています。

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

## 検証 {#section_5F1783F5FE2644F1B94B0101F73D57EB}

### 広告開始

個々の広告再生の開始時に、次の順番で 3 件の重要な呼び出しが送信されます。

1. ビデオ広告分析開始
1. ハートビート広告開始
1. ハートビート分析開始

呼び出し 1 および 2 には、カスタムと標準の両方の追加のメタデータ変数が含まれます。

### 広告再生

広告再生中、Heartbeat Ad Play 呼び出しが 1 秒間隔でハートビートサーバーに送信されます。

### 広告完了

広告がすべて再生されると、Heartbeat Ad Complete 呼び出しが送信されます。

### 広告スキップ

広告がスキップされた場合は、イベントが送信されないので、トラッキングコールに広告情報が含まれません。

>[!TIP]
>
>広告の時間開始と広告の時間完了時に一意の呼び出しが送信されません。

