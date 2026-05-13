---
title: チャプターとセグメントをトラッキングする方法
description: メディア SDK を使用したチャプターおよびセグメント追跡の実装方法です。
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 97%

---

# 概要{#overview}

以下の手順は、SDK 2.x を使用した実装についてのガイダンスです。

>[!IMPORTANT]
> 
> 1.x バージョンの SDK を実装する場合は、開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

チャプターおよびセグメントの追跡は、カスタム定義されたメディアのチャプターまたはセグメントに対して使用できます。 チャプターの追跡は一般的に、メディアコンテンツ（野球のイニングなど）に基づくカスタムセグメントの定義や、広告ブレークの間のコンテンツセグメントの定義に使用されます。 コアメディア追跡の実装では、チャプター追跡は&#x200B;**不要です**。

チャプターの追跡には、チャプター開始、チャプター完了、チャプタースキップが含まれます。 このメディアプレーヤー API をカスタマイズしたセグメント化ロジックと共に使用して、チャプターイベントを識別したり、必須およびオプションのチャプター変数を設定したりできます。

## プレーヤーイベント

### チャプター開始時

* チャプターのチャプターオブジェクトのインスタンス `chapterObject` を作成します
* チャプターのメタデータ `chapterCustomMetadata` を設定します
* を呼び出します `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### チャプター完了時

* を呼び出します `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### チャプタースキップ時

* を呼び出します `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## チャプター追跡の実装 {#implement-chapter-tracking}

1. いつチャプター開始イベントが発生するかを識別し、チャプター情報を使用して `ChapterObject` インスタンスを作成します。

   以下に、`ChapterObject` チャプター追跡リファレンスを示します。

   >[!NOTE]
   >
   >これらの変数は、チャプターを追跡する場合にのみ必要です。

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | 章名 | ○ |
   | `position` | 章の位置 | ○ |
   | `length` | 章の長さ | ○ |
   | `startTime` | 章の開始時間 | ○ |

1. チャプターのカスタムメタデータを含める場合、そのメタデータのコンテキストデータ変数を作成します。
1. チャプター再生の追跡を開始するには、`ChapterStart` インスタンスで `MediaHeartbeat` イベントを呼び出します。
1. カスタムコードで定義したチャプター終了の境界まで再生したら、`ChapterComplete` インスタンスで `MediaHeartbeat` イベントを呼び出します。
1. ユーザーがチャプターをスキップした（例えば、ユーザーがチャプター境界の外にシークした）のでチャプター再生が完了しなかった場合は、MediaHeartbeat インスタンスで `ChapterSkip` イベントを呼び出します。
1. その他のチャプターがある場合、手順 1 ～ 5 を繰り返します。

以下のサンプルコードでは、HTML5 メディアプレーヤー用の JavaScript 2.x SDK を使用しています。 このコードをコアメディア再生コードと共に使用する必要があります。

```js
/* Call on chapter start */
if (e.type == "chapter start") {
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500);
    /* Set custom context data*/
    var chapterCustomMetadata = {
        segmentType:"Baseball Innings",
        segmentName:"Inning 5",
        segmentInfo:"Game Six"
    }
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata);
};

/* Call on chapter complete */
if (e.type == "chapter complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};

/* Call on chapter skip */
if (e.type == "chapter skip") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```
