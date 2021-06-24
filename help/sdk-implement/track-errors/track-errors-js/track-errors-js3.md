---
title: JavaScript 3.xを使用したエラーの追跡方法を説明します。
description: ブラウザーアプリ(JS)でのメディアSDKを使用したエラー追跡の実装について説明します。
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 78%

---

# JavaScript 3.x を使用したエラーの追跡{#track-errors-on-javascript}

>[!IMPORTANT]
>
>以下の手順は、すべての 3.x SDK に共通する実装のガイダンスです。以前のバージョンの SDK を実装している場合は、[SDK のダウンロード](/help/sdk-implement/download-sdks.md)から開発者ガイドをダウンロードできます。

## エラー追跡の実装

1. メディアプレーヤーのエラーを追跡します。

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError` の呼び出しの後で `trackSessionEnd` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。
