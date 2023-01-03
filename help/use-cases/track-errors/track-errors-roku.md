---
title: Roku でエラーをトラッキングする方法
description: Roku で Media SDK を使用してエラートラッキングを実装する方法を説明します。
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '94'
ht-degree: 100%

---

# Roku でのエラーの追跡 {#track-errors-on-roku}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
> 1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

## エラー追跡の実装

1. メディアプレーヤーのエラーを追跡します。

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(),
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError` の呼び出しの後で `trackSessionEnd` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。
