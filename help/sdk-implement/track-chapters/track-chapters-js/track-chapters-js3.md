---
title: JavaScript 3.x を使用したチャプターとセグメントのトラッキング
description: ブラウザーアプリ（JS）で Media SDK を使用してチャプターとセグメントのトラッキングを実装する方法を説明します。
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 100%

---

# JavaScript 3.x を使用したチャプターおよびセグメントの追跡{#track-chapters-and-segments-on-javascript}

以下の手順は、SDK 3.x を使用した実装についてのガイダンスです。

>[!IMPORTANT]
>
> 以前のバージョンの SDK を実装している場合は、[SDK のダウンロード](/help/sdk-implement/download-sdks.md)から開発者ガイドをダウンロードできます。

1. いつチャプター開始イベントが発生するかを識別し、チャプター情報を使用して `ChapterObject` インスタンスを作成します。

   `ChapterObject` チャプター追跡リファレンス：

   >[!NOTE]
   >
   >これらの変数は、チャプターを追跡する場合にのみ必要です。

   | 変数名 | タイプ | 説明 |
   | --- | --- | --- |
   | `name` | string | チャプター名を示す空白以外の文字列。 |
   | `position` | 数値 | コンテンツ内のチャプターの位置（1 から始まります）。 |
   | `length` | 数値 | チャプターの長さを示す正の数。 |
   | `startTime` | 数値 | チャプターの開始位置の再生ヘッド値。 |

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
