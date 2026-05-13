---
title: JavaScript 3.x を使用してバッファリングをトラッキングする方法
description: ブラウザーアプリ（JS）でバッファリングイベントをトラッキングする方法を説明します。
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Bq0X19pW-5gWyLJMkst3zlEXUjZRYm2Yw9JqxJvuTZw
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 123
ht-degree: 100%

---

# JavaScript 3.x を使用したバッファリングの追跡{#track-buffering-on-javascript}

以下の手順は、すべての 3.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>以前のバージョンの SDK を実装している場合は、[SDK のダウンロード](/help/getting-started/download-sdks.md)から開発者ガイドをダウンロードできます。

## バッファー追跡の定数

| 定数名 | 説明     |
|---|---|
| `BufferStart` | 追跡する Buffer Start イベントの定数 |
| `BufferComplete` | 追跡する Buffer Complete イベントの定数 |

## バッファリングの実装

1. メディアプレーヤーの再生バッファーイベントをリッスンし、バッファー開始イベント通知時に、`BufferStart` イベントを使用してバッファーを追跡します。

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. メディアプレーヤーからのバッファー完了通知時に、`BufferComplete` イベントを使用してバッファーの終わりを追跡します。

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

詳しくは、追跡シナリオの[バッファリングがある VOD 再生](/help/use-cases/tracking-scenarios/vod-buffering.md)を参照してください。
