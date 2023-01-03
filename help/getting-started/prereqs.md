---
title: ストリーミングメディアの前提条件について説明します
description: Adobe Analytics Streaming Media の基本を学ぶ。 Adobe Analytics for Streaming Media の実装に必要な事項について説明します。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b022bed6b7be0cc97caaaf6b7bbc42474a57b400
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 96%

---

# 前提条件{#prerequisites}

Adobe Analytics for Streaming Media を実装するには、次のタスクを実行します。

1. **Steaming Media の価格モデルを確認する**<br>
現在の価格モデルは、ビデオストリームに基づいています。Streaming Media Analytics は Adobe Analytics とは別売なので、必要に応じて、営業担当または販売店に連絡して、新しい販売注文に署名してください。

1. **Adobe Analytics の実装を確認する**<br> Streaming Media for Adobe Analytics には、Adobe Analytics の基本的な実装も必要です。詳しくは、[Adobe Analytics の実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja)を参照してください。

1. **メディアトラッキングサーバーの URL を取得する**<br> メディアトラッキングサーバーの URL については、Adobe Analytics の営業担当または販売店にお問い合わせください。 この 
`collection-api-server` URL は、Mobile SDK 用、JavaScript SDK 用および Roku の非収集 APIトラッキングサーバー用です。API 実装のドメイン名は、`[your_namespace].hb-api.omtrdc.net` です。

1. **現在の Media SDK をダウンロードするか、必要な拡張機能を実装する**<br> 実装パスに応じて、web、モバイルまたは OTT（オーバーザトップ）プラットフォーム用の[最新の SDK をダウンロード](download-sdks.md)します。ストリーミングメディア用 Adobe Analytics拡張機能のパスを有効にするには、必要な拡張機能を実装する必要があります。

1. **Adobe Analytics レポートを有効にする**<br> Analytics でレポートを有効にし、収集しているコンテンツや広告データを表示するには、Analytics でレポートを有効にする必要があります。 詳しくは、 [メディアレポートの有効化](/help/reporting/media-reports-enable.md).

1. **Experience Cloud を有効にする**<br>


## Adobe Experience Platform ID サービスの実装 {#implement-id}

**ID サービス**&#x200B;は、Experience Cloud コアサービス、ソリューション、People コアサービスの顧客属性およびオーディエンスのための、共通の識別フレームワークです。ID サービスは、サイト訪問者に一意の永続的な ID を割り当てることで機能します。組織が ID サービスを実装している場合、この ID を使用すれば、異なる Experience Cloud ソリューション内で、同じサイト訪問者と彼らのデータを識別できます。

![ID サービスのグラフィック](assets/mc_id_service_graphic.png)

ID サービスは、様々なソリューション固有の ID（例えば、Analytics AID）を置き換えることもできます。[顧客 ID と認証状態](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=ja)機能を使用すると、ID サービスを通じて顧客 ID を Experience Cloud に渡すことが可能になります。ただし、ID サービスは、既に登録されているソリューションのみと連携することに注意してください。他製品へのアクセスにサインアップしていない場合、ID サービスではアクセスが提供されません。

ID サービスは、多くの Experience Cloud 機能、機能強化、サービスにとって不可欠なコンポーネントです。 現在、ID サービスは、[Analytics](https://www.adobe.com/jp/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/jp/marketing-cloud/data-management-platform.html) および [Target](https://www.adobe.com/jp/marketing-cloud/testing-targeting.html) をサポートしています。

ID サービスを実装していない場合、今が移行戦略を検討し始めるチャンスです。ID サービスの重要性と役割について詳しくは、[なぜ新しい Identity Service に注目すべきか](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)を参照してください。

Experience Cloud ID について詳しくは、[Experience Cloud ID の概要](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=ja)および [Adobe Experience Platform ID サービス](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja) を参照してください。
