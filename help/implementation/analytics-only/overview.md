---
title: Analyticsのみの実装の概要
description: Analyticsのみの実装に使用される、ストリーミングメディア用Adobe Analytics アドオンの前提条件と実装方法。
feature: Streaming Media
role: User, Admin, Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 5%
---
# Analyticsのみの実装の概要

Analyticsのみの実装では、Adobe Analytics for Streaming Media アドオンを使用して、Edge Networkを使用せずにAdobe Analyticsに直接データを送信します。 これらの方法は引き続き完全にサポートされています。 新しい実装の場合は、Adobeでは[Edgeの実装](/help/implementation/edge/overview.md)をお勧めします。これは、Adobe Analyticsに加えてCustomer Journey Analytics、Adobe Journey Optimizer、Real-Time CDPでデータを利用できるためです。

## 前提条件

1. **一般的な前提条件を完了します。** [一般的な前提条件](/help/getting-started/prereqs.md)を参照してください。

1. **Adobe Analyticsの実装を確認します。** Analyticsのみのストリーミングメディアの実装には、基本的なAdobe Analyticsの実装が必要です。 [Adobe Analyticsの実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)を参照してください。

1. **メディアトラッキングサーバーのURLを取得します。** Adobe Analyticsの担当者に、メディアトラッキングサーバーのURL （`collection-api-server` URL）を尋ねます。 ドメインは通常、パターン `[your_namespace].hb-api.omtrdc.net`に従います。

1. **SDKをダウンロードするか、拡張機能をインストールします。** プラットフォームによっては、[現在のSDK](/help/getting-started/download-sdks.md)をダウンロードするか、必要なタグ拡張機能をインストールします。

## 実装方法の選択

各ページでは、ストリーミングメディア固有の設定について説明します。 イベントごとのコードと変数ごとのコードは、[ イベント ](/help/implementation/events/overview.md)および[変数](/help/implementation/variables/overview.md)にあります。

| Codebase | インコード | タグの使用 |
|---|---|---|
| Web （JavaScript） | [JavaScript](javascript.md) | [Media Analytics タグ拡張機能](javascript-tags.md) |
| Chromecast | [Chromecast](chromecast.md) | — |
| Roku | [Roku 2.x](roku-2x.md) | — |
| API | [Media Collection API](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/implementation) | — |

## 次の手順

実装が完了したら、[Analyticsのみの実装用のレポートを設定できます](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [実装の概要](/help/implementation/overview.md)
>* [ イベントの概要](/help/implementation/events/overview.md)
>* [変数の概要](/help/implementation/variables/overview.md)
