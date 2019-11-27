---
title: Chromecast でのエラーの追跡
description: ここでは、Chromecast でのメディア SDK を使用したエラー追跡の実装について説明します。
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Chromecast でのエラーの追跡 {#track-errors-on-chromecast}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

## エラー追跡の実装

1. メディアプレーヤーのエラー [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError) を追跡します。

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError` の呼び出しの後で `trackSessionEnd` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。

