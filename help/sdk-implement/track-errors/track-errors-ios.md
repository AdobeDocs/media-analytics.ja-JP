---
title: iOS でのエラーの追跡
description: ここでは、iOS でのメディア SDK を使用したエラー追跡の実装について説明します。
uuid: 18ea93d3-5948-4375-bcdb-72309268e38d
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# iOS でのエラーの追跡 {#track-errors-on-ios}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

## エラー追跡の実装

1. メディアプレーヤーのエラーを追跡します。

   ```
   - (void)onPlayerError:(NSNotification *)notification { 
       [_mediaHeartbeat trackError:@"mediaoErrorId"]; 
   }
   ```

>[!NOTE]
>
>メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError` の呼び出しの後で `trackSessionEnd` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。

