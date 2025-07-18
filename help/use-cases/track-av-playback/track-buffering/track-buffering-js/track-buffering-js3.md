---
title: JavaScript 3.x を使用してバッファリングをトラッキングする方法
description: ブラウザーアプリ（JS）でバッファリングイベントをトラッキングする方法を説明します。
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '120'
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
