---
title: JavaScript 3.x を使用してエラーをトラッキングする方法
description: ブラウザーアプリ（JS）で Media SDK を使用してエラートラッキングを実装する方法を説明します。
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# JavaScript 3.x を使用したエラーの追跡{#track-errors-on-javascript}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>以前のバージョンの SDK を実装している場合は、[SDK のダウンロード](/help/getting-started/download-sdks.md)から開発者ガイドをダウンロードできます。

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
