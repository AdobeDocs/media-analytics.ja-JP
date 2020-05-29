---
title: JavaScript 3.xを使用したチャプターとセグメントの追跡
description: ここでは、ブラウザーアプリ（JS）でのメディア SDK を使用したチャプターおよびセグメント追跡の実装について説明します。
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 71%

---


# JavaScript 3.xを使用したチャプターとセグメントの追跡{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>以下の手順は、SDK 3.x を使用した実装についてのガイダンスです。If you are implementing any previous versions of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. いつチャプター開始イベントが発生するかを識別し、チャプター情報を使用して `ChapterObject` インスタンスを作成します。

   `ChapterObject` チャプター追跡リファレンス：

   >[!NOTE]
   >
   >これらの変数は、チャプターを追跡する場合にのみ必要です。

   | 変数名 | タイプ | 説明 |
   | --- | --- | --- |
   | `name` | string | チャプター名を示す空以外の文字列。 |
   | `position` | 数値 | コンテンツ内のチャプターの位置（1から始まる）。 |
   | `length` | 数値 | チャプターの長さを示す正の数。 |
   | `startTime` | 数値 | チャプターの開始時の再生ヘッドの値 |

   チャプターオブジェクト：

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. チャプターのカスタムメタデータを含める場合、そのメタデータのコンテキストデータ変数を作成します。

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. チャプター再生の追跡を開始するには、`ChapterStart` インスタンスで `MediaHeartbeat` イベントを呼び出します。

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. カスタムコードで定義したチャプター終了の境界まで再生したら、`ChapterComplete` インスタンスで `MediaHeartbeat` イベントを呼び出します。

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. ユーザーがチャプターをスキップした（例えば、ユーザーがチャプター境界の外にシークした）のでチャプター再生が完了しなかった場合は、MediaHeartbeat インスタンスで `ChapterSkip` イベントを呼び出します。

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. その他のチャプターがある場合、手順 1 ～ 5 を繰り返します。
