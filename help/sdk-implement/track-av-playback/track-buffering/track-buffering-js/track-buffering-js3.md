---
title: JavaScript 3.x を使用したバッファーの追跡
description: ブラウザーアプリ（JS）でのバッファーの追跡イベントを説明します。
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '115'
ht-degree: 100%

---

# JavaScript 3.x を使用したバッファーの追跡 {#track-buffering-on-javascript}

>[!IMPORTANT]
>
>以下の手順は、すべての 3.x SDK に共通する実装のガイダンスです。以前のバージョンの SDK を実装している場合は、[SDK のダウンロード](/help/sdk-implement/download-sdks.md)から開発者ガイドをダウンロードできます。

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

詳しくは、追跡シナリオの[バッファリングがある VOD 再生](/help/sdk-implement/tracking-scenarios/vod-buffering.md)を参照してください。
