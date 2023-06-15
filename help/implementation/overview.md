---
title: ストリーミングメディアのAdobe AnalyticsまたはCustomer Journey Analyticsへの実装
description: ストリーミングメディアの実装パスについて説明します。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: ade20d7ae3cbb525b3a8390a27e1d93201d83003
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Streaming Media for Adobe Analytics の実装 またはCustomer Journey Analytics

ストリーミングメディアは様々な方法で実装できます。 このページで説明している実装方法でサポートされるデバイスとプラットフォームの詳細な比較については、 [サポートされるデバイスとプラットフォーム](/help/getting-started/supported-devices.md).

## Edge 実装メソッド

ほとんどの場合、新しいAdobe AnalyticsまたはCustomer Journey Analytics(CJA) のすべてのお客様に対して Media Analytics を実装する際には、Edge を使用することをお勧めします。

* **Media for Edge Network SDK / Extension:** iOSおよび Android デバイスからデータを収集し、Edge に送信します。 その後、データを CJA またはAdobe Analyticsに送信できます。

  Media for Edge Network SDK/Extension について詳しくは、 [Media Edge を使用した Media Analytics のExperience Platform](/help/implementation/implementation-edge.md).

  >[!NOTE]
  >
  >この実装方法は、現在、Web SDK または Roku をサポートしていません。 ただし、Media Edge API を使用して実装する場合は、両方ともサポートされます。

* **Media Edge API:** 任意のデバイスまたは形式（モバイル、Web、上位のデバイスを含む）からデータを収集し、Edge にデータを送信するようにカスタマイズできます。 その後、データを CJA またはAdobe Analyticsに送信できます。

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![CJA ワークフロー](assets/cja-implementation.png)

## その他の実装方法

ほとんどの場合、特に新しい実装では、CJA とAdobe Analyticsの両方で、上記の Edge 実装方法をお勧めします。

Edge 実装方法に加えて、他の実装方法も使用できます。 これらの実装方法は、最初、Adobe Analyticsで使用するように設計されました。 ただし、次のいずれかの実装方法を使用するお客様は、 [Analytics ソース接続](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=ja).

* **タグ付きのメディア拡張機能：** Adobe MediumAnalytics for Audio and Video 拡張機能は、タグが有効なサイトまたはプロジェクトにメディアトラッカーインスタンスを追加する機能を提供します。 データがAdobe Analyticsに送信されます。

  タグを使用したメディア拡張機能のインストール、設定および実装について詳しくは、 [Adobe MediumAnalytics (3.x SDK) for Audio and Video 拡張機能の概要](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **メディア SDK:**  データがAdobe Analyticsに送信されます。

  Media SDK と拡張機能のダウンロードとインストールについて詳しくは、[Media SDK、タグを使用した拡張機能、OTT SDK の取得](/help/getting-started/download-sdks.md)を参照してください。

* **メディアコレクション API:** RESTful HTTP 呼び出しを使用して、オーディオおよびビデオイベントを追跡します。 データがAdobe Analyticsに送信されます。

  Media Collection API の使用について詳しくは、[Media Collection API](media-collection-api/mc-api-overview.md) を参照してください。


![Analytics ワークフロー](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
