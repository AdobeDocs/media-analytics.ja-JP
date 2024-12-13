---
title: Adobe Analytics のみの実装の前提条件
description: Adobe Analyticsのみの実装またはEdge実装で Streaming Media Collection を使用するための前提条件を説明します
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 10%

---

# Edge の実装の前提条件

この節で説明する前提条件は、Edge実装を使用した Streaming Media Collection Adobeの実装に固有です。

1. **一般的な前提条件を満たす**<br>
Streaming Media Collection をAdobe Analyticsのみの実装用に実装する場合でも、Edge実装の場合でも、[ 一般的な前提条件 ](/help/getting-started/prereqs.md) を満たしていることを確認してください。

1. **Edge Networkおよびストリーミングメディアコレクションと互換性のあるAdobeソリューションを実装していることを確認してください**<br>
Edgeを使用して Streaming Media Collection を実装する場合、Customer Journey Analytics（Adobe Analytics、Adobe Journey OptimizerまたはReal-time Customer Data Platform）も機能している必要があります。 詳しくは、次のドキュメントリソースを参照してください。
   * [Customer Journey Analytics ガイド](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=ja)
   * [Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)
   * [Adobe Journey Optimizer ドキュメント ](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
   * [Real-time Customer Data Platform ドキュメント ](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=ja)

1. **メディアトラッキングサーバーの URL の取得**<br>
Customer Journey Analytics担当者にメディアトラッキングサーバーの URL を問い合わせてください。<!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Edge Networkを使用した Streaming Media Collection の実装**<br>
[Edge Networkを使用したストリーミングメディアコレクションの実装 ](/help/implementation/edge/implementation-edge.md) の手順に従います。
