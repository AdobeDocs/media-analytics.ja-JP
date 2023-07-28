---
title: ストリーミングメディアの前提条件について説明します
description: Adobe Analytics Streaming Media の基本を学ぶ。 Adobe Analytics for Streaming Media の実装に必要な事項について説明します。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 75%

---

# 前提条件 {#prerequisites}

ストリーミングメディアの実装を開始する前に、次のタスクを実行します。

1. **ストリーミングメディアの概要の確認**<br>
ストリーミングメディアの実装を開始する前に、 [ストリーミングメディア：概要](/help/media-overview.md) を使用して、ストリーミングメディアがニーズを満たしていることを確認します。

1. **Steaming Media の価格モデルを確認する**<br>
現在の価格モデルは、ビデオストリームに基づいています。Streaming Media Analytics はAdobe Analyticsとは別売なので、必要に応じて、営業担当者またはAdobeのアカウントチームに連絡し、新しい販売注文に署名してください。

1. **Adobe Analytics レポートを有効にする**<br> Analytics でレポートを有効にし、収集しているコンテンツや広告データを表示するには、Analytics でレポートを有効にする必要があります。 [メディアレポートの有効化](/help/reporting/media-reports-enable.md)を参照してください。

1. **Experience CloudへのAdobe Experience Platform Identity Service の実装**

   **ID サービス**&#x200B;は、Experience Cloud コアサービス、ソリューション、People コアサービスの顧客属性およびオーディエンスのための、共通の識別フレームワークです。ID サービスは、サイト訪問者に一意の永続的な ID を割り当てることで機能します。組織が ID サービスを実装している場合、この ID を使用すれば、異なる Experience Cloud ソリューション内で、同じサイト訪問者と彼らのデータを識別できます。

   ![ID サービスのグラフィック](assets/mc_id_service_graphic.png)

   ID サービスは、様々なソリューション固有の ID（例えば、Analytics AID）を置き換えることもできます。[顧客 ID と認証状態](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=ja)機能を使用すると、ID サービスを通じて顧客 ID を Experience Cloud に渡すことが可能になります。ただし、ID サービスは、既に登録されているソリューションのみと連携することに注意してください。他製品へのアクセスにサインアップしていない場合、ID サービスではアクセスが提供されません。

   ID サービスは、多くの Experience Cloud 機能、機能強化、サービスにとって不可欠なコンポーネントです。 現在、ID サービスは、[Analytics](https://www.adobe.com/jp/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/jp/marketing-cloud/data-management-platform.html) および [Target](https://www.adobe.com/jp/marketing-cloud/testing-targeting.html) をサポートしています。

   ID サービスを実装していない場合、今が移行戦略を検討し始めるチャンスです。ID サービスの重要性と役割について詳しくは、[なぜ新しい Identity Service に注目すべきか](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)を参照してください。

   Experience Cloud ID について詳しくは、[Experience Cloud ID の概要](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=ja)および [Adobe Experience Platform ID サービス](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja) を参照してください。

1. **実装方法のその他の前提条件を表示します**

   ストリーミングメディアの実装方法に応じて、次のいずれかの実装方法の前提条件を確認します。

   * [Adobe Analyticsのみの実装の前提条件](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * Edge 実装の前提条件
