---
title: Adobe Analytics のみの実装の前提条件
description: Adobe Analyticsのみの実装またはEdge実装で Streaming Media Collection アドオンを使用するための前提条件を説明します
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 10%

---

# Edge の実装の前提条件

この節で説明する前提条件は、Edge実装を使用したAdobeのストリーミングメディアコレクションアドオンの実装に固有です。

1. **一般的な前提条件を満たす**<br>
Streaming Media Collection アドオンをAdobe Analyticsのみの実装に実装する場合でも、Edgeの実装に実装する場合でも、を満たしていることを確認してください [一般的な前提条件](/help/getting-started/prereqs.md).

1. **Edge Networkおよびストリーミングメディアコレクションアドオンと互換性のあるAdobeソリューションを実装していることを確認します**<br>
Edgeを使用して Streaming Media Collection アドオンを実装する場合、Customer Journey Analytics（Adobe Analytics、Adobe Journey OptimizerまたはReal-time Customer Data Platform）も機能している必要があります。 詳しくは、次のドキュメントリソースを参照してください。
   * [Customer Journey Analytics ガイド](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=ja)
   * [Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)
   * [Adobe Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
   * [Real-time Customer Data Platform ドキュメント](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=ja)

1. **メディアトラッキングサーバーの URL の取得**<br>
メディアトラッキングサーバーの URL については、Customer Journey Analytics担当者にお問い合わせください。 <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Edge Networkを使用した Streaming Media Collection アドオンの実装**<br>
の手順に従います [Edge Networkを使用した Streaming Media Collection アドオンの実装](/help/implementation/edge/implementation-edge.md).
