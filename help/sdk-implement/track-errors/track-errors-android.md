---
seo-title: Android でのエラーの追跡
title: Android でのエラーの追跡
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Android でのエラーの追跡{#track-errors-on-android}

>[!IMPORTANT]
>
>以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. メディアプレイヤーのエラーの追跡：

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>メディアプレイヤーのエラーを追跡しても、メディアトラッキングセッションは停止しません。 If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

