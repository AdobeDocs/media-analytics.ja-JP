---
title: Android でのエラーの追跡
description: ここでは、Android でのメディア SDK を使用したエラー追跡の実装について説明します。
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Android でのエラーの追跡 {#track-errors-on-android}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/sdk-implement/download-sdks.md)）からダウンロードできます。

1. メディアプレーヤーのエラーを追跡します。

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError` の呼び出しの後で `trackSessionEnd` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。

