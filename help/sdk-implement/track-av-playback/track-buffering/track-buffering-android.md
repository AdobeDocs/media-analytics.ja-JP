---
seo-title: Android でのバッファーの追跡
title: Android でのバッファーの追跡
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Android でのバッファーの追跡{#track-buffering-on-android}

>[!IMPORTANT]
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDks.](../../../sdk-implement/download-sdks.md)

## バッファートラッキング定数

| 定数名 | 説明     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | 追跡する Buffer Start イベントの定数 |
| `MediaHeartbeat.Event.BufferComplete` | 追跡する Buffer Complete イベントの定数 |

## バッファリングの実装

1. メディアプレーヤーの再生バッファーイベントをリッスンし、バッファー開始イベント通知時に、`BufferStart` イベントを使用してバッファーを追跡します。

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
   }
   ```

1. メディアプレーヤーからのバッファー完了通知時に、`BufferComplete` イベントを使用してバッファーの終わりを追跡します。

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
   }
   ```

詳しくは、追跡シナリオの[バッファリングがある VOD 再生](../../../sdk-implement/tracking-scenarios/vod-buffering.md)を参照してください。
