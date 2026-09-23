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
    internal-label: Analytics
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
    internal-label: Reports
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
    internal-label: Implementations
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
subfeature_v2:
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
    internal-label: Methods
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 10%
---
# 前提条件 {#prerequisites}

Adobe ストリーミングメディアサービスの実装を開始する前に、次のタスクを実行します。

1. **価格モデルを確認**<br>
Customer Journey Analytics Streaming Media Collection アドオンおよびAdobe Analytics for Streaming Media アドオンの現在の価格モデルは、ビデオストリームに基づいています。 アドオンはAdobe AnalyticsとAdobe Experience Platformで別途販売されるため、必要に応じて営業担当者またはAdobeのアカウントチームにお問い合わせください。

1. **Adobe Analytics レポートを有効にする** *（Analyticsのみの実装）*<br>
Analyticsでレポートを有効にし、収集するコンテンツと広告データを表示するには、レポートを有効にする必要があります。 「[Analyticsのみの実装に対するレポートの設定](/help/reporting/setup/analytics-reporting.md)」を参照してください。

1. **IDの設定**<br>

   IDの設定要件は、実装方法によって異なります。

   * **Edgeの実装**: IDは、Adobe Experience Platform ID名前空間設定を通じて処理されます。 訪問者ID サービスを個別に設定する必要はありません。 詳しくは、[Edgeの実装の概要](/help/implementation/edge/overview.md)を参照してください。

   * **Analyticsのみの実装**: CX Enterprise ソリューション全体で一貫して訪問者を識別するには、Adobe Visitor ID サービスを有効にする必要があります。 訪問者ID サービスは、各サイト訪問者に一意の永続的なIDを割り当て、そのIDを購読するすべてのCX Enterprise ソリューション間で共有できるようにします。

     詳しくは、[Adobe Visitor ID サービスのドキュメント &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja)を参照してください。

1. **実装方法の追加の前提条件を表示する**

   ストリーミングメディアサービスの実装方法に応じて、次のいずれかの実装方法の前提条件を確認します。

   * [Analyticsのみの実装の概要](/help/implementation/analytics-only/overview.md)

   * [Edgeの導入の概要](/help/implementation/edge/overview.md)

   適切な実装方法を判断するには、[実装の概要](/help/implementation/overview.md)を参照してください。
