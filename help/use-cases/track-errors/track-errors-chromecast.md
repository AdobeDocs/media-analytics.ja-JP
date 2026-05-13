---
title: Chromecast でエラーをトラッキングする方法
description: Chromecast で Media SDK を使用してエラートラッキングを実装する方法を説明します。
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
exl-id: 513772c2-582d-4b4b-92ed-0c32b99d7fdc
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LK23AdaTrN-oQw6JVfPDUCuZOyIi9G3Sjbmr9WmC-Kk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 108
ht-degree: 100%

---

# Chromecast でのエラーの追跡{#track-errors-on-chromecast}

以下の手順は、すべての 2.x SDK に共通する実装のガイダンスです。

>[!IMPORTANT]
>
>1.x バージョンの SDK を実装する場合は、1.x の開発ガイドをこちら（[SDK のダウンロード](/help/getting-started/download-sdks.md)）からダウンロードできます。

## エラー追跡の実装

1. メディアプレーヤーのエラー [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError) を追跡します。

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>メディアプレーヤーのエラーの追跡は、メディアトラッキングセッションを停止しません。 メディアプレーヤーのエラーが再生の続行を妨げる場合、`trackError` の呼び出しの後で `trackSessionEnd` を呼び出すことで、メディアトラッキングセッションを確実に終了するようにしてください。
