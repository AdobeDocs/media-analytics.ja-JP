---
title: Chromecast でのチャプターおよびセグメントの追跡
description: このトピックでは、ChromecastでのMedia SDKを使用したチャプターおよびセグメントトラッキングの実装について説明します。
uuid: 5ea562b9-0e07-4fbb-9a3b-213d746304f5
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Chromecast でのチャプターおよびセグメントの追跡{#track-chapters-and-segments-on-chromecast}

>[!IMPORTANT]
>
>以下の手順は、2.x SDKを使用した実装のガイダンスを示しています。 If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. いつチャプター開始イベントが発生するかを識別し、チャプター情報を使用して `ChapterObject` インスタンスを作成します。

   `ChapterObject` チャプタートラッキングリファレンス：

   >[!NOTE]
   >
   >これらの変数は、チャプターを追跡する予定の場合にのみ必要です。

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | チャプター名 | ○ |
   | `position` | チャプター位置 | ○ |
   | `length` | チャプターの長さ | ○ |
   | `startTime` | チャプター開始時間 | ○ |

   チャプターオブジェクト：[createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createChapterObject)

   ```js
   chapterInfo = ADBMobile.media.createChapterObject("First Chapter", 1, CHAPTER1_LENGTH, CHAPTER1_START_POS);
   ```

1. チャプターのカスタムメタデータを含める場合、そのメタデータのコンテキストデータ変数を作成します。

   ```js
   var chapterContextData = { 
       segmentType: "Sample segment type" 
   };
   ```

1. チャプター再生の追跡を開始するには、`ChapterStart` イベントを追跡します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, ChapterInfo, chapterContextData); 
   ```

1. カスタムコードで定義したチャプター終了の境界まで再生したら、`ChapterComplete` インスタンスで `MediaHeartbeat` イベントを呼び出します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
   ```

1. ユーザーがチャプターをスキップした（例えば、ユーザーがチャプター境界の外にシークした）のでチャプター再生が完了しなかった場合は、`ChapterSkip` イベントを呼び出します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip); 
   ```

1. その他のチャプターがある場合、手順 1 ～ 5 を繰り返します。

