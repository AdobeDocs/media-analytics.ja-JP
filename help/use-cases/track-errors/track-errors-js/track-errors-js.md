---
title: JavaScript 2.x を使用してエラーをトラッキングする方法
description: ブラウザーアプリ（JS）で Media SDK を使用してエラートラッキングを実装する方法を説明します。
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
exl-id: b3012bce-4b92-408e-8b7a-57ae9d52e93d
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 100%

---

# JavaScript 2.x を使用したエラーの追跡{#track-errors-on-javascript}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

## エラー追跡の実装

1. メディアプレーヤーのエラーを追跡します。

   ```js
   onPlayerError = function() {
       this._mediaHeartbeat.trackError("mediaErrorId");
   };
   ```

>[!NOTE]
>
>メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError` の呼び出しの後で `trackSessionEnd` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。
