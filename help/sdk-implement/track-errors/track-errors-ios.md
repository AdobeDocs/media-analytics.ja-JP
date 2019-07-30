---
seo-title: iOS でのエラーの追跡
title: iOS でのエラーの追跡
uuid: 18ea93d3-5948-4375- bcdb-72309268e38d
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# iOS でのエラーの追跡{#track-errors-on-ios}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## エラー追跡の実装

1. メディアプレイヤーのエラーの追跡:

   ```
   - (void)onPlayerError:(NSNotification *)notification { 
       [_mediaHeartbeat trackError:@"mediaoErrorId"]; 
   }
   ```

>[!NOTE]
>
>メディアプレイヤーのエラーを追跡しても、メディアトラッキングセッションは停止しません。If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

