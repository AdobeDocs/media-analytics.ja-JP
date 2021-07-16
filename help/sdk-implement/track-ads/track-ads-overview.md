---
title: 広告の追跡の説明
description: メディア SDK を使用した広告トラッキングの実装の概要です。
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 99%

---

# 概要{#overview}

以下の手順は、SDK 2.x を使用した実装についてのガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

広告再生には、広告ブレーク、広告開始、広告完了、広告スキップの追跡が含まれます。メディアプレーヤーの API を使用して、重要なプレーヤーイベントを識別したり、必須およびオプションの広告変数を設定したりできます。メタデータの包括的なリストについては、[広告パラメーター](/help/metrics-and-metadata/ad-parameters.md)を参照してください。

## プレーヤーイベント {#player-events}


### 広告ブレークの開始時

>[!NOTE]
>プリロールを含みます

* 広告ブレークの `adBreak` オブジェクトインスタンスを作成します。例：`adBreakObject`。

* `adBreakObject` を使用して、広告ブレーク開始の `trackEvent` を呼び出します。

### すべての広告アセットの開始時

* 広告アセットの広告オブジェクトインスタンスを作成します。例：`adObject`。
* 広告のメタデータ `adCustomMetadata` を設定します。
* 広告開始の `trackEvent` を呼び出します。

### すべての広告の完了時

* 広告完了の `trackEvent` を呼び出します。

### 広告スキップ時

* 広告スキップの `trackEvent` を呼び出します。

### 広告ブレークの完了時

* ブレーク完了の `trackEvent` を呼び出します。

## 広告トラッキングの実装 {#implement-ad-tracking}

### 広告トラッキングの定数

| 定数名 | 説明   |
|---|---|
| `AdBreakStart` | 追跡する AdBreak Start イベントの定数 |
| `AdBreakComplete` | 追跡する AdBreak Complete イベントの定数 |
| `AdStart` | 追跡する Ad Start イベントの定数 |
| `AdComplete` | 追跡する Ad Complete イベントの定数 |
| `AdSkip` | 追跡する Ad Skip イベントの定数 |

### 実装手順

1. プリロールを含め、いつ広告ブレークの境界が開始するかを識別し、広告ブレーク情報を使用して `AdBreakObject` を作成します。

   `AdBreakObject` リファレンス：

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | プリロール、ミッドロール、ポストロールなど、広告ブレークの名前 | ○ |
   | `position` | コンテンツ内の広告ブレークの位置番号（1 から始まる）。 | ○ |
   | `startTime` | 広告ブレーク開始時の再生ヘッド値 | ○ |

1. `MediaHeartbeat` インスタンスの `AdBreakStart` で `trackEvent()` を呼び出し、広告ブレークの追跡を開始します。

1. いつ広告が開始するかを識別し、広告情報を使用して `AdObject` インスタンスを作成します。

   `AdObject` リファレンス：

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | 広告のわかりやすい名前. | ○ |
   | `adId` | 広告の一意の ID。 | ○ |
   | `position` | 広告ブレーク内の広告の位置番号（1 から始まる）。 | ○ |
   | `length` | 広告の長さ | ○ |

1. オプションで、コンテキストデータ変数を使用して標準または広告メタデータをトラッキングセッションにアタッチします。

   * **標準広告メタデータ** - 標準広告メタデータの場合、ご利用のプラットフォームのキーを使用して、標準広告メタデータのキーと値のペアのディクショナリを作成します。
   * **カスタムの広告メタデータ** - カスタムのメタデータの場合は、カスタムデータ変数の変数オブジェクトを作成し、現在の広告のデータを設定します。

1. `MediaHeartbeat` インスタンスの `AdStart` イベントで `trackEvent()` を呼び出し、広告再生の追跡を開始します。

   カスタムメタデータ変数（または空のオブジェクト）への参照を、イベント呼び出しの 3 番目のパラメーターとして追加します。

1. 広告の再生が広告の終わりに到達したら、`AdComplete` イベントで `trackEvent()` を呼び出します。

1. ユーザーが広告のスキップを選択したので広告再生が完了しなかった場合は、`AdSkip` イベントを追跡します。
1. 同じ `AdBreak` にその他の広告がある場合、手順 3 ～ 7 を繰り返します。
1. 広告ブレークが完了したら、`AdBreakComplete` イベントを使用して追跡します。

>[!IMPORTANT]
>
>広告の再生（`s:asset:type=ad`）中、コンテンツプレーヤーの再生ヘッド（`l:event:playhead`）を増分しないでください。増分すると、コンテンツ視聴時間指標に悪影響をおよぼします。

以下のサンプルコードでは、HTML5 メディアプレーヤー用の JavaScript 2.x SDK を使用しています。

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
