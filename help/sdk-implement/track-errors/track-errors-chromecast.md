---
seo-title: Chromecast でのエラーの追跡
title: Chromecast でのエラーの追跡
uuid: efa9de8d- c626-4cb6- b46d-108495dd013a
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Chromecast でのエラーの追跡{#track-errors-on-chromecast}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## エラー追跡の実装

1. Track media player errors: [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>メディアプレイヤーのエラーを追跡しても、メディアトラッキングセッションは停止しません。If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

