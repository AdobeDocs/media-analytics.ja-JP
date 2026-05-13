---
title: 広告のトラッキング
description: メディア SDK を使用した広告トラッキングの実装の概要です。
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 510
ht-degree: 79%

---

# 概要{#overview}

以下の手順は、SDK 2.x を使用した実装についてのガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

広告再生には、広告ブレーク、広告開始、広告完了、広告スキップの追跡が含まれます。 メディアプレーヤーの API を使用して、重要なプレーヤーイベントを識別したり、必須およびオプションの広告変数を設定したりできます。

## プレーヤーイベント {#player-events}

### 広告ブレークの開始時

>[!NOTE]
>プリロールを含みます

* 広告ブレークの `adBreak` オブジェクトインスタンスを作成します。 例：`adBreakObject`。

* `adBreakObject` を使用して、広告ブレーク開始の `trackEvent` を呼び出します。

### すべての広告アセットの開始時

* 広告アセットの広告オブジェクトインスタンスを作成します。 例：`adObject`。
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
   | `name` | プリロール、ミッドロール、ポストロールなどの広告ブレーク名。 | ○ |
   | `position` | コンテンツ内の広告ブレークの位置（1から始まる）。 | ○ |
   | `startTime` | 広告ブレーク開始時の再生ヘッド値 | ○ |

1. `MediaHeartbeat` インスタンスの `AdBreakStart` で `trackEvent()` を呼び出し、広告ブレークの追跡を開始します。

1. いつ広告が開始するかを識別し、広告情報を使用して `AdObject` インスタンスを作成します。

   `AdObject` リファレンス：

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | 広告のわかりやすい名前. | ○ |
   | `adId` | 広告の一意のID。 | ○ |
   | `position` | 広告ブレーク内の広告の位置を1から始めます。 | ○ |
   | `length` | 広告の長さ | ○ |

1. オプションで、コンテキストデータ変数を使用して、標準および/または広告メタデータをトラッキングセッションに添付できます。

   * **標準広告メタデータ -**&#x200B;標準広告メタデータの場合、プラットフォームのキーを使用して、標準広告メタデータキー値ペアのディクショナリを作成します。
   * **カスタム広告メタデータ -** カスタムメタデータの場合は、カスタムデータ変数用の変数オブジェクトを作成し、現在の広告のデータを入力します。

1. `MediaHeartbeat` インスタンスの `AdStart` イベントで `trackEvent()` を呼び出し、広告再生の追跡を開始します。

   カスタムメタデータ変数（または空のオブジェクト）への参照を、イベント呼び出しの 3 番目のパラメーターとして追加します。

1. 広告の再生が広告の終わりに到達したら、`AdComplete` イベントで `trackEvent()` を呼び出します。

1. ユーザーが広告のスキップを選択したので広告再生が完了しなかった場合は、`AdSkip` イベントを追跡します。
1. 同じ `AdBreak` にその他の広告がある場合、手順 3 ～ 7 を繰り返します。
1. 広告ブレークが完了したら、`AdBreakComplete` イベントを使用して追跡します。

>[!IMPORTANT]
>
>広告の再生（`s:asset:type=ad`）中、コンテンツプレーヤーの再生ヘッド（`l:event:playhead`）を増分しないでください。 増分すると、コンテンツ視聴時間指標に悪影響をおよぼします。

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
