---
title: Android でバッファリングをトラッキングする方法
description: Android でバッファリングイベントをトラッキングする方法を説明します。
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 100%

---

# Android でのバッファーの追跡{#track-buffering-on-android}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

## バッファー追跡の定数

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

詳しくは、追跡シナリオの[バッファリングがある VOD 再生](/help/use-cases/tracking-scenarios/vod-buffering.md)を参照してください。
