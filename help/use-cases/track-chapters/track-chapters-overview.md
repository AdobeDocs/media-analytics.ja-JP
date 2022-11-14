---
title: チャプターとセグメントをトラッキングする方法
description: メディア SDK を使用したチャプターおよびセグメント追跡の実装方法です。
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 100%

---

# 概要 {#overview}

以下の手順は、SDK 2.x を使用した実装についてのガイダンスです。

>[!IMPORTANT]
> 
> 1.x バージョンの SDK を実装する場合は、開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

チャプターおよびセグメントの追跡は、カスタム定義されたメディアのチャプターまたはセグメントに対して使用できます。チャプターの追跡は一般的に、メディアコンテンツ（野球のイニングなど）に基づくカスタムセグメントの定義や、広告ブレークの間のコンテンツセグメントの定義に使用されます。コアメディア追跡の実装では、チャプター追跡は&#x200B;**不要です**。

チャプターの追跡には、チャプター開始、チャプター完了、チャプタースキップが含まれます。このメディアプレーヤー API をカスタマイズしたセグメント化ロジックと共に使用して、チャプターイベントを識別したり、必須およびオプションのチャプター変数を設定したりできます。

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
   | `name` | チャプター名 | ○ |
   | `position` | チャプター位置 | ○ |
   | `length` | チャプターの長さ | ○ |
   | `startTime` | チャプター開始時間 | ○ |

1. チャプターのカスタムメタデータを含める場合、そのメタデータのコンテキストデータ変数を作成します。
1. チャプター再生の追跡を開始するには、`ChapterStart` インスタンスで `MediaHeartbeat` イベントを呼び出します。
1. カスタムコードで定義したチャプター終了の境界まで再生したら、`ChapterComplete` インスタンスで `MediaHeartbeat` イベントを呼び出します。
1. ユーザーがチャプターをスキップした（例えば、ユーザーがチャプター境界の外にシークした）のでチャプター再生が完了しなかった場合は、MediaHeartbeat インスタンスで `ChapterSkip` イベントを呼び出します。
1. その他のチャプターがある場合、手順 1 ～ 5 を繰り返します。

以下のサンプルコードでは、HTML5 メディアプレーヤー用の JavaScript 2.x SDK を使用しています。このコードをコアメディア再生コードと共に使用する必要があります。

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
