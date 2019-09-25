---
seo-title: Android でのシークの追跡
title: Android でのシークの追跡
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Android でのシークの追跡{#track-seeking-on-android}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## シークトラッキング定数

| 定数名 | 説明     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | 追跡する Seek Start イベントの定数。 |
| `MediaHeartbeat.Event.SeekComplete` | 追跡する Seek Complete イベントの定数。 |

## Implement seeking

1. メディアプレーヤーの再生シークイベントをリッスンし、シーク開始イベント通知時に、`SeekStart` イベントを使用してシークを追跡します。

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. メディアプレーヤーからのシーク完了通知時に、`SeekComplete` イベントを使用してシークの終わりを追跡します。

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

詳しくは、追跡シナリオの[メインコンテンツでのシークのある VOD 再生](/help/sdk-implement/tracking-scenarios/vod-seeking.md)を参照してください。
