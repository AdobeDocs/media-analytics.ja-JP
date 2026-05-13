---
title: Adobe Analytics のみの実装の前提条件
description: Adobe Analyticsのみの実装またはEdgeの実装でストリーミングメディアコレクションを使用するための前提条件について説明します
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
TQID: https://experienceleague.adobe.com/OqimGafihuirpnAaZ4AvrX2lrOmCtr0FLXk3QwoVTew
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 19%

---

# Edge の実装の前提条件

この節で説明する前提条件は、Edge実装を使用してAdobe Streaming Media Collectionを実装する場合に固有です。

1. **一般的な前提条件を完了する**<br>
Adobe Analyticsのみの実装またはEdgeの実装にStreaming Media Collectionを実装する場合でも、[一般的な前提条件](/help/getting-started/prereqs.md)を満たしていることを確認してください。

1. **Edge NetworkおよびStreaming Media Collectionと互換性のあるAdobe ソリューションを導入していることを確認してください**<br>
Edgeを使用してStreaming Media Collectionを実装する場合は、Customer Journey Analytics、Adobe Analytics、Adobe Journey Optimizer、またはReal-Time Customer Data Platformを実装している必要があります。 詳しくは、次のドキュメントリソースを参照してください。
   * [Customer Journey Analytics ガイド](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=ja)
   * [Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)
   * [Adobe Journey Optimizer ドキュメント](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ja)
   * [Real-Time Customer Data Platform ドキュメント](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html?lang=ja)

1. **メディアトラッキングサーバーのURLを取得**<br>
Customer Journey Analyticsの担当者に、メディアトラッキングサーバーのURLを尋ねます。<!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Edge Networkを使用したStreaming Media Collectionの実装**<br>
[Edge Networkを使用したStreaming Media Collectionの実装](/help/implementation/edge/implementation-edge.md)の手順に従います。
