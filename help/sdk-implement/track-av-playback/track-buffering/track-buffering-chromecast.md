---
title: Chromecast でのバッファーの追跡
description: Chromecastでのバッファリングイベントの追跡について説明します。
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Chromecast でのバッファーの追跡{#track-buffering-on-chromecast}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## バッファートラッキング定数


| 定数名 | 説明     |
|---|---|
| `BufferStart` | 追跡する Buffer Start イベントの定数 |
| `BufferComplete` | 追跡する Buffer Complete イベントの定数 |

## バッファリングの実装

1. メディアプレーヤーの再生バッファーイベントをリッスンし、バッファー開始イベント通知時に、`BufferStart` イベントを使用してバッファーを追跡します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. メディアプレーヤーからのバッファー完了通知時に、`BufferComplete` イベントを使用してバッファーの終わりを追跡します（[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)）。

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

詳しくは、追跡シナリオの[バッファリングがある VOD 再生](/help/sdk-implement/tracking-scenarios/vod-buffering.md)を参照してください。
