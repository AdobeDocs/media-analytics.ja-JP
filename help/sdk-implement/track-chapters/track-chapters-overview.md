---
title: 概要
description: Media SDKを使用したチャプターおよびセグメントトラッキングの実装方法。
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 概要{#overview}

>[!IMPORTANT]
>
>以下の手順は、2.x SDKを使用した実装のガイダンスを示しています。 If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

チャプターおよびセグメントの追跡は、カスタム定義のメディアチャプターまたはセグメントで使用できます。 チャプタートラッキングの一般的な使用方法は、メディアコンテンツに基づいてカスタムセグメントを定義する場合や、広告の時間の間にコンテンツセグメントを定義する場合です。 Chapter tracking is **not** required for core media tracking implementations.

チャプターの追跡には、チャプター開始、チャプター完了、チャプタースキップが含まれます。メディアプレイヤーAPIをカスタマイズされたセグメントロジックと共に使用して、チャプターイベントを識別し、必要なチャプター変数とオプションのチャプター変数を設定できます。

## プレーヤーイベント

### チャプター開始時

* チャプターのチャプターオブジェクトのインスタンス `chapterObject` を作成します
* Populate the chapter metadata, `chapterCustomMetadata`
* 呼び出し `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### チャプター完了時

* 呼び出し `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### チャプタースキップ時

* 呼び出し `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## チャプタートラッキングの実装 {#implement-chapter-tracking}

1. いつチャプター開始イベントが発生するかを識別し、チャプター情報を使用して `ChapterObject` インスタンスを作成します。

   以下に、`ChapterObject` チャプター追跡リファレンスを示します。

   >[!NOTE]
   >
   >これらの変数は、チャプターを追跡する予定の場合にのみ必要です。

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

以下のサンプルコードは、HTML5メディアプレイヤー用のJavaScript 2.x SDKを使用しています。 このコードは、コアメディア再生コードと共に使用する必要があります。

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

