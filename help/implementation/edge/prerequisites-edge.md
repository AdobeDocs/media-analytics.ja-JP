---
title: Adobe Analyticsのみの実装の前提条件
description: Adobe Analyticsのみの実装でストリーミングメディアを使用するための前提条件について説明します。
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 16%

---

# Edge 実装の前提条件

この節で説明する前提条件は、Edge 実装を使用したストリーミングメディアの実装に固有です。

1. **一般的な前提条件の完了**<br>
ストリーミングメディアをAdobe Analyticsのみの実装に実装する場合も、Edge の実装に実装する場合も、 [一般的な前提条件](/help/getting-started/prereqs.md).

1. **Edge およびストリーミングメディアと互換性のあるAdobeソリューションを実装していることを確認する**<br>
Edge を使用してストリーミングメディアを実装する場合は、作業Customer Journey Analytics、Adobe Analytics、Adobe Journey Optimizer、Real-time Customer Data Platformの実装も必要です。 詳しくは、次のドキュメントリソースを参照してください。
   * [Customer Journey Analytics ガイド](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=ja)
   * [Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)
   * [Adobe Journey Optimizerドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
   * [Real-time Customer Data Platformドキュメント](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=ja)

1. **メディアトラッキングサーバーの URL を取得する**<br>
メディアトラッキングCustomer Journey Analyticsの URL については、サーバーの担当者にお問い合わせください。 <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Edge での Media Analytics のインストール**<br>
次の手順に従います： [Media Edge を使用した Media Analytics のExperience Platform](/help/implementation/edge/implementation-edge.md).