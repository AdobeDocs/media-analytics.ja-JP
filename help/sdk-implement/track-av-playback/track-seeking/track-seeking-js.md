---
seo-title: JavaScript でのシークの追跡
title: JavaScript でのシークの追跡
uuid: 089947fb-8bae-4ae8- b215-53793620efd7
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# JavaScript でのシークの追跡{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../../sdk-implement/download-sdks.md)

## シークトラッキング定数

| 定数名 | 説明     |
|---|---|
| `SeekStart` | 追跡する Seek Start イベントの定数。 |
| `SeekComplete` | 追跡する Seek Complete イベントの定数。 |

## シークの実装

1. メディアプレーヤーの再生シークイベントをリッスンし、シーク開始イベント通知時に、`SeekStart` イベントを使用してシークを追跡します。

   ```js
   _onSeekStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
   };
   ```

1. メディアプレーヤーからのシーク完了通知時に、`SeekComplete` イベントを使用してシークの終わりを追跡します。

   ```js
   _onSeekComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
   };
   ```

詳しくは、追跡シナリオの[メインコンテンツでのシークのある VOD 再生](../../../sdk-implement/tracking-scenarios/vod-seeking.md)を参照してください。
