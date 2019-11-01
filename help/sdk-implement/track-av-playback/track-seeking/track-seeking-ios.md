---
title: iOS でのシークの追跡
description: ここでは、iOSでのMedia SDKを使用したシークトラッキングの実装について説明します。
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# iOS でのシークの追跡{#track-seeking-on-ios}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## シークトラッキング定数

| 定数名 | 説明     |
|---|---|
| `ADBMediaHeartbeatEventSeekStart` | 追跡する Seek Start イベントの定数。 |
| `ADBMediaHeartbeatEventSeekComplete` | 追跡する Seek Complete イベントの定数。 |

## シークの実装

1. メディアプレーヤーの再生シークイベントをリッスンし、シーク開始イベント通知時に、`SeekStart` イベントを使用してシークを追跡します。

   ```
   - (void)onSeekStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. メディアプレーヤーからのシーク完了通知時に、`SeekComplete` イベントを使用してシークの終わりを追跡します。

   ```
   - (void)onSeekComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

詳しくは、追跡シナリオの[メインコンテンツでのシークのある VOD 再生](/help/sdk-implement/tracking-scenarios/vod-seeking.md)を参照してください。
