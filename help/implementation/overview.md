---
title: Adobe Analytics または Customer Journey Analytics 用のストリーミングメディアの実装
description: ストリーミングメディアの実装パスについて説明します。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 984f058fda15b1c5e960e4c8d8e2378308d2b541
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 81%

---

# Streaming Media for Adobe Analytics の実装または Customer Journey Analytics

ストリーミングメディアは様々な方法で実装できます。このページで説明している実装方法でサポートされるデバイスとプラットフォームの比較について詳しくは、[サポートされるデバイスとプラットフォーム](/help/getting-started/supported-devices.md)を参照してください。

## Edge の実装方法

Adobe Analytics または Customer Journey Analytics のすべての新規顧客に対して Media Analytics を実装する場合は、Edge を使用することをお勧めします。

* **Edge Network 用 Media SDK／拡張機能：** iOS および Android デバイスからデータを収集し、Edge に送信します。その後、データを Customer Journey Analytics または Adobe Analytics に送信できます。

  Edge Network 用 Media SDK／拡張機能について詳しくは、[Experience Platform Edge を使用した Media Analytics のインストール](/help/implementation/edge/implementation-edge.md)を参照してください。

  >[!NOTE]
  >
  >この実装方式は現在、Web SDK または Roku をサポートしていません。ただし、Media Edge API を使用して実装する場合は両方ともサポートされます。

* **Media Edge API：**&#x200B;任意のデバイスまたは形式（モバイル、web、オーバーザトップデバイスなど）からデータを収集し、Edge にデータを送信するようにカスタマイズできます。その後、データを Customer Journey Analytics または Adobe Analytics に送信できます。

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![CJA ワークフロー](assets/cja-implementation.png)

## Adobe Analytics のみの実装方式

上記の Edge 実装方式は、Customer Journey Analytics と Adobe Analytics の両方、特に新しい実装の場合に推奨されます。

Edge 実装方式に加えて、他の実装方式も使用できます。これらの実装方式は、Adobe Analytics で使用するために設計されました。ただし、次のいずれかの実装方法を使用している既存の顧客は、[Analytics ソース接続](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=ja)を作成することで、Customer Journey Analytics でデータを使用できるようにすることができます。

* **タグ付きのメディア拡張機能：** Adobe Medium Analytics for Audio and Video 拡張機能は、タグが有効なサイトまたはプロジェクトにメディアトラッカーインスタンスを追加する機能を提供します。データは Adobe Analytics に送信されます。

  タグ付きのメディア拡張機能のインストール、設定、実装について詳しくは、[Adobe Media Analytics (3.x SDK) for Audio and Video 拡張機能の概要](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html?lang=ja)を参照してください。

* **メディア SDK:**  メディア SDK を使用すると、Web サイト、携帯電話、接続された TV、タブレット、OTT デバイス、セットトップボックス、ゲームコンソールなど、複数のメディアプラットフォームを測定できます。 ( 詳しくは、 [サポートされるデバイスとプラットフォーム](/help/getting-started/supported-devices.md).)

  メディア SDK は、メディアコレクション API を追跡に使用します。 データは Adobe Analytics に送信されます。

  Media SDK と拡張機能のダウンロードとインストールについて詳しくは、[Media SDK、タグを使用した拡張機能、OTT SDK の取得](/help/getting-started/download-sdks.md)を参照してください。

* **メディアコレクション API:** メディアコレクション API はカスタマイズ可能なので、カスタムトラッキング機能を必要とするアプリケーションや、メディア SDK でサポートされていないデバイスに使用できます。 メディアコレクション API は、RESTful HTTP 呼び出しを使用してオーディオおよびビデオイベントを追跡します。 データは Adobe Analytics に送信されます。

  Media Collection API の使用について詳しくは、[Media Collection API](media-collection-api/mc-api-overview.md) を参照してください。


![Analytics ワークフロー](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
