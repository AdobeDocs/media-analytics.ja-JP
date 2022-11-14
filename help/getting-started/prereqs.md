---
title: ストリーミングメディアの前提条件について説明します
description: Adobe Analytics Streaming Media の基本を学ぶ。 Adobe Analytics for Streaming Media の実装に必要な事項について説明します。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 50%

---

# 前提条件{#prerequisites}

ストリーミングメディア用Adobe Analyticsを実装するには、次のタスクを実行します。

1. **ストリーミングメディアの価格モデルを確認する**<br>
現在の価格モデルは、ビデオストリームに基づいています。 Streaming Media Analytics はAdobe Analyticsとは別売なので、必要に応じて、営業担当またはアカウントマネージャーに連絡して、新しい販売注文に署名してください。

1. **Adobe Analyticsの実装を確認する**<br>
Adobe Analytics向けストリーミングメディアには、Adobe Analyticsの基本的な実装も必要です。 詳しくは、 [Adobe Analyticsの実装](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ja) を参照してください。

1. **メディアトラッキングサーバーの URL を取得します**<br>
メディアトラッキングサーバーの URL については、Adobe Analyticsの担当者にお問い合わせください。 この 
`collection-api-server` モバイル SDK、JavaScript SDK および Roku 用の非コレクション API トラッキングサーバーの URL。 API 実装のドメイン名は次のとおりです。 `[your_namespace].hb-api.omtrdc.net`.

1. **現在のメディア SDK をダウンロードするか、必要な拡張機能を実装します。**<br>
実装パスに応じて、 [現在の SDK をダウンロード](download-sdks.md) web、モバイル、またはオーバーザトッププラットフォームの場合。 Adobe Analytics for Streaming Media を有効にするには、必要な拡張機能を実装する必要があります。 必要な拡張機能について詳しくは、 [Adobe拡張](download-sdks.md#media-extension). （メディア SDK のダウンロードまたは拡張機能の取得を明確にする必要がある）

1. **Adobe Analytics Reports を有効にする**<br>
Analytics でレポートを有効にし、収集しているコンテンツや広告データを表示するには、Analytics でレポートを有効にする必要があります。 詳しくは、 [メディアレポートの有効化。](/help/reporting/media-reports-enable.md).

1. **「Enable」Experience Cloud**<br>


## Adobe Experience Platform ID サービスの実装. {#implement-id}

この **ID サービス** は、People コアサービスのExperience Cloudコアサービス、ソリューション、顧客属性およびオーディエンスのための、共通の識別フレームワークを有効にします。 ID サービスは、サイト訪問者に一意の永続的な ID を割り当てることで機能します。組織が ID サービスを実装している場合、この ID を使用すれば、異なる Experience Cloud ソリューション内で、同じサイト訪問者と彼らのデータを識別できます。

![ID サービスのグラフィック](assets/mc_id_service_graphic.png)

ID サービスは、様々なソリューション固有の ID（例えば、Analytics AID）を置き換えることもできます。[顧客 ID と認証状態](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=ja)機能を使用すると、ID サービスを通じて顧客 ID を Experience Cloud に渡すことが可能になります。ただし、ID サービスは、既に登録されているソリューションのみと連携することに注意してください。他製品へのアクセスにサインアップしていない場合、ID サービスではアクセスが提供されません。

ID サービスは、多くのExperience Cloud機能、機能強化、サービスにとって不可欠な要素です。 現在、ID サービスは、[Analytics](https://www.adobe.com/jp/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/jp/marketing-cloud/data-management-platform.html) および [Target](https://www.adobe.com/jp/marketing-cloud/testing-targeting.html) をサポートしています。

ID サービスを実装していない場合、今が移行戦略を検討し始めるチャンスです。ID サービスの重要性と役割について詳しくは、[なぜ新しい Identity Service に注目すべきか](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)を参照してください。

Experience Cloud ID について詳しくは、[Experience Cloud ID の概要](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=ja)および [Adobe Experience Platform ID サービス](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ja) を参照してください。
