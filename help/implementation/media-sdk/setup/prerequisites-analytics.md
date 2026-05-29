---
title: Adobe Analytics のみの実装の前提条件
description: Adobe Analyticsのみの実装でAdobe Analytics for Streaming Media アドオンを使用するための前提条件について説明します
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
TQID: https://experienceleague.adobe.com/falbDtUtqAMtmtQs2jLpEvUKmwvATotVu8njuTNZ09k
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
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
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: 243
ht-degree: 14%

---

# Adobe Analytics のみの実装の前提条件

この節で説明する前提条件は、（Edgeを使用しない場合に）Adobe-Analyticsのみの実装用のAdobe Analytics for Streaming Media アドオンの実装に固有のものです。

1. **一般的な前提条件を完了する**<br>
Adobe Analyticsのみの実装にストリーミングメディアサービスを実装する場合でも、Edgeの実装に対してストリーミングメディアサービスを実装する場合でも、[一般的な前提条件](/help/getting-started/prereqs.md)を満たしていることを確認してください。

1. **Adobe Analyticsを実装していることを確認してください**<br>
Analyticsのみの実装用にAdobe Analytics for Streaming Media アドオンを実装する場合は、Adobe Analyticsの基本実装も必要です。 詳しくは、[Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)を参照してください。

1. **メディアトラッキングサーバーのURLを取得**<br>
メディアトラッキングサーバーのURLについては、Adobe Analytics担当者にお問い合わせください。 これは、モバイル SDK、JavaScript SDK、Roku用の非collection-api トラッキングサーバーの`collection-api-server` URLです。 API 実装のドメイン名は、`[your_namespace].hb-api.omtrdc.net` です。

1. **現在のMedia SDKをダウンロードするか、必要な拡張機能を実装します**<br>
実装パスに応じて、[現在のSDK](/help/getting-started/download-sdks.md)をweb、モバイル、またはオーバーザトップのプラットフォーム用にダウンロードします。 Adobe Analytics for Streaming Media アドオンを有効にするには、必要な拡張機能を実装する必要があります。

1. **Adobe Analytics レポートの有効化**<br>
Analyticsでレポートを有効にし、収集するコンテンツと広告データを表示するには、Analyticsでレポートを有効にする必要があります。 [メディアレポートの有効化](/help/implementation/media-sdk/setup/media-reports-enable.md)を参照してください。
