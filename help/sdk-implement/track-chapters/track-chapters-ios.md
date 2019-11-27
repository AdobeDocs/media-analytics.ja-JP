---
title: iOS でのチャプターおよびセグメントの追跡
description: ここでは、iOS でのメディア SDK を使用したチャプターおよびセグメント追跡の実装について説明します。
uuid: ffc5ce9f-04ba-4059-92d4-4cb4180ac9ed
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# iOS でのチャプターおよびセグメントの追跡 {#track-chapters-and-segments-on-ios}

>[!IMPORTANT]
>
>以下の手順は、SDK 2.x を使用した実装についてのガイダンスです。1.x バージョンの SDK を実装する場合は、開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

1. いつチャプター開始イベントが発生するかを識別し、チャプター情報を使用して `ChapterObject` インスタンスを作成します。

   `ChapterObject` チャプター追跡リファレンス：

   >[!NOTE]
   >
   >これらの変数は、チャプターを追跡する場合にのみ必要です。

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | チャプター名 | ○ |
   | `position` | チャプター位置 | ○ |
   | `length` | チャプターの長さ | ○ |
   | `startTime` | チャプター開始時間 | ○ |

   チャプターオブジェクト：

   ```
   id chapterObject =  
     [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME] 
                        position:[POSITION] 
                        length:[LENGTH] 
                        startTime:[START_TIME]];
   ```

1. チャプターのカスタムメタデータを含める場合、そのメタデータのコンテキストデータ変数を作成します。

   ```
   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init]; 
   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"]; 
   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"]; 
   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
   ```

1. チャプター再生の追跡を開始するには、`ChapterStart` インスタンスで `MediaHeartbeat` イベントを呼び出します。

   ```
   - (void)onChapterStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary]; 
   }
   ```

1. カスタムコードで定義したチャプター終了の境界まで再生したら、`ChapterComplete` インスタンスで `MediaHeartbeat` イベントを呼び出します。

   ```
   - (void)onChapterComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. ユーザーがチャプターをスキップした（例えば、ユーザーがチャプター境界の外にシークした）のでチャプター再生が完了しなかった場合は、MediaHeartbeat インスタンスで `ChapterSkip` イベントを呼び出します。

   ```
   - (void)onChapterSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. その他のチャプターがある場合、手順 1 ～ 5 を繰り返します。

