---
title: Adobe ストリーミングメディアサービスの前提条件について説明します
description: ストリーミングメディアサービスの概要。 Adobe Experience Manager Sitesの導入に必要なもの。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 491
ht-degree: 66%

---

# 前提条件 {#prerequisites}

Adobe ストリーミングメディアサービスの実装を開始する前に、次のタスクを実行します。

1. **Adobe ストリーミングメディアサービスの概要を確認する**<br>
ストリーミングメディアサービスの導入を開始する前に、[Adobe ストリーミングメディアサービスの概要](/help/media-overview.md)を確認して、ニーズを満たしていることを確認してください。

1. **価格モデルを確認**<br>
Customer Journey Analytics Streaming Media Collection アドオンおよびAdobe Analytics for Streaming Media アドオンの現在の価格モデルは、ビデオストリームに基づいています。 アドオンはAdobe AnalyticsとAdobe Experience Platformで別途販売されるため、必要に応じて営業担当者またはAdobeのアカウントチームにお問い合わせください。

1. **Adobe Analytics レポートの有効化**<br>
AnalyticsまたはCustomer Journey Analyticsでレポートを有効にし、収集するコンテンツと広告データを表示するには、レポートを有効にする必要があります。 [メディアレポートの有効化](/help/reporting/media-reports-enable.md)を参照してください。

1. **Experience Cloud に Adobe Experience Platform ID サービスを実装する**

   **ID サービス**&#x200B;は、Experience Cloud コアサービス、ソリューション、People コアサービスの顧客属性およびオーディエンスのための、共通の識別フレームワークです。 ID サービスは、サイト訪問者に一意の永続的な ID を割り当てることで機能します。 組織が ID サービスを実装している場合、この ID を使用すれば、異なる Experience Cloud ソリューション内で、同じサイト訪問者と彼らのデータを識別できます。

   ![ID サービスのグラフィック](assets/mc_id_service_graphic.png)

   ID サービスは、様々なソリューション固有の ID（例えば、Analytics AID）を置き換えることもできます。 [顧客 ID と認証状態](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=ja)機能を使用すると、ID サービスを通じて顧客 ID を Experience Cloud に渡すことが可能になります。 ただし、ID サービスは、既に登録されているソリューションのみと連携することに注意してください。 他製品へのアクセスにサインアップしていない場合、ID サービスではアクセスが提供されません。

   ID サービスは、多くの Experience Cloud 機能、機能強化、サービスにとって不可欠なコンポーネントです。 現在、ID サービスは、[Analytics](https://www.adobe.com/jp/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/jp/marketing-cloud/data-management-platform.html) および [Target](https://www.adobe.com/jp/marketing-cloud/testing-targeting.html) をサポートしています。

   ID サービスを実装していない場合、今が移行戦略を検討し始めるチャンスです。 ID サービスの重要性と役割について詳しくは、[なぜ新しい Identity Service に注目すべきか](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)を参照してください。

   Experience Cloud ID について詳しくは、[Experience Cloud ID の概要](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=ja)および [Adobe Experience Platform ID サービス](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja) を参照してください。

1. **実装方法の追加の前提条件を表示する**

   ストリーミングメディアサービスの実装方法に応じて、次のいずれかの実装方法の前提条件を確認します。

   * [Adobe Analytics のみの実装の前提条件](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Edge の実装の前提条件](/help/implementation/edge/prerequisites-edge.md)

   適切な実装方法を判断するには、[実装の概要](/help/implementation/overview.md)を参照してください。
