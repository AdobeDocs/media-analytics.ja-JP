---
seo-title: Android でのチャプターおよびセグメントの追跡
title: Android でのチャプターおよびセグメントの追跡
uuid: 013815d7-4d9e-48f4- a2b9-3b70cb1149d3
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Android でのチャプターおよびセグメントの追跡{#track-chapters-and-segments-on-android}

>[!IMPORTANT]
>
>次の手順では、2. x SDKを使用した導入について説明します。If you are implementing a 1.x version of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## チャプタートラッキングの実装

1. いつチャプター開始イベントが発生するかを識別し、チャプター情報を使用して `ChapterObject` インスタンスを作成します。

   `ChapterObject` チャプタートラッキングリファレンス:

   >[!NOTE]
   >
   >これらの変数は、チャプターを追跡する計画がある場合にのみ必要です。

   | 変数名 | 説明 | 必須 |
   | --- | --- | :---: |
   | `name` | チャプター名 | ○ |
   | `position` | チャプター位置 | ○ |
   | `length` | チャプターの長さ | ○ |
   | `startTime` | チャプター開始時間 | ○ |

   チャプターオブジェクト：

   ```java
   MediaObject chapterDataInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. チャプターのカスタムメタデータを含める場合、そのメタデータのコンテキストデータ変数を作成します。

   ```java
   HashMap<String, String> chapterMetadata =  
     new HashMap<String,String>(); 
   chapterMetadata.put("segmentType", "Sample Segment Type"); 
   chapterMetadata.put("segmentName", "Sample Segment Name"); 
   chapterMetadata.put("segmentInfo", "Sample Segment Info");
   ```

1. チャプター再生の追跡を開始するには、`ChapterStart` インスタンスで `MediaHeartbeat` イベントを呼び出します。

   ```java
   public void onChapterStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                             chapterDataInfo,  
                             chapterMetadata); 
   }
   ```

1. カスタムコードで定義したチャプター終了の境界まで再生したら、`ChapterComplete` インスタンスで `MediaHeartbeat` イベントを呼び出します。

   ```java
   public void onChapterComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null); 
   }
   ```

1. ユーザーがチャプターをスキップした（例えば、ユーザーがチャプター境界の外にシークした）のでチャプター再生が完了しなかった場合は、MediaHeartbeat インスタンスで `ChapterSkip` イベントを呼び出します。

   ```java
   public void onChapterSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null); 
   }
   ```

1. その他のチャプターがある場合、手順 1 ～ 5 を繰り返します。

