---
title: JavaScript でのエラーの追跡
description: ここでは、ブラウザーアプリ(JS)でMedia SDKを使用してエラートラッキングを実装する方法について説明します。
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# JavaScript でのエラーの追跡{#track-errors-on-javascript}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## エラー追跡の実装

1. メディアプレイヤーのエラーの追跡：

   ```js
   onPlayerError = function() { 
       this._mediaHeartbeat.trackError("mediaErrorId"); 
   };
   ```

>[!NOTE]
>
>メディアプレイヤーのエラーを追跡しても、メディアトラッキングセッションは停止しません。 If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

