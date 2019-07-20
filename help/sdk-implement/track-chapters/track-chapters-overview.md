---
seo-title: 概要
title: 概要
uuid: 3fe32425-5e2a-4886-8fea- d91d15671bb0
translation-type: tm+mt
source-git-commit: b461da1823e45eef86302e14501eac0d4b055c7a

---


# 概要{#overview}

>[!IMPORTANT]
>
>次の手順では、2. x SDKを使用した導入について説明します。If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](../../sdk-implement/download-sdks.md)

チャプターとセグメントの追跡は、カスタム定義のメディアチャプターまたはセグメントで使用できます。チャプタートラッキングの一般的な使用法は、メディアコンテンツ（野球の休止など）に基づいてカスタムセグメントを定義したり、広告の時間間でコンテンツセグメントを定義したりすることです。Chapter tracking is **not** required for core media tracking implementations.

チャプターの追跡には、チャプター開始、チャプター完了、チャプタースキップが含まれます。メディアプレイヤーAPIをカスタマイズしたセグメント化ロジックで使用して、チャプターイベントを識別したり、必須およびオプションのチャプター変数を設定したりできます。

## プレーヤーイベント

### チャプター開始時

* チャプターのチャプターオブジェクトのインスタンス `chapterObject` を作成します
* Populate the chapter metadata, `chapterCustomMetadata`
* 呼び出し `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### チャプター完了時

* 呼び出し `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### チャプタースキップ時

* 呼び出し `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implement chapter tracking {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. いつチャプター開始イベントが発生するかを識別し、チャプター情報を使用して `ChapterObject` インスタンスを作成します。

   以下に、`ChapterObject` チャプター追跡リファレンスを示します。

   >[!NOTE]
   >
   >これらの変数は、チャプターを追跡する計画がある場合にのみ必要です。

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

以下のサンプルコードでは、HTML5メディアプレイヤー用のJavaScript2. x SDKを使用しています。このコードは、コアメディア再生コードで使用する必要があります。

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

## 検証 {#section_07EC2811BE3249249494596BFE9BF869}

### チャプター開始

個々のチャプター再生の開始時に、1回のキー呼び出しが送信されます。

* ハートビートチャプター開始（この呼び出しには、チャプターメタデータ変数が追加されています）

### チャプター完了

チャプターの終了境界では、ハートビートチャプター完了呼び出しが送信されます。

### チャプタースキップ

チャプターがスキップされると、ハートビートチャプタースキップ呼び出しが送信されます。
