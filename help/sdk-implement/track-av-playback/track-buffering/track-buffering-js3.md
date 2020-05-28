---
title: JavaScript 3.xを使用したバッファリングの追跡
description: ブラウザーアプリ（JS）でのバッファーの追跡イベントを説明します。
translation-type: tm+mt
source-git-commit: 8235fee973623c168dbf83f43aa85f13b4e06cff
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 74%

---


# JavaScript 3.xを使用したバッファリングの追跡{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>以下の手順は、すべての 3.x SDK に共通する実装のガイダンスです。If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

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
