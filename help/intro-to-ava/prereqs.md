---
title: 前提条件
description: 前提条件
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
source-git-commit: e56ce73316d9cf00193220df8959a489fc3f2124
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 89%

---

# 前提条件{#prerequisites}

## 判断 {#decision}

トラッキングの実装を開始する前に、どの実装が状況に最も適しているかを、早期に決定する必要があります。

* **Media Analytics** - 最新のメディア SDK（標準、推奨される実装）やメディアコレクション API（RESTful）を使用
* **マイルストーン** - 以前のアドビのトラッキング実装
* **データ挿入 API** - メディア SDK を使用しないトラッキングの実装

## タスク {#prereq-tasks}

*Media Analytics* 実装について、開始前に完了しておく必要がある作業を示します。

1. **Experience Cloud を有効にします。**

   Adobe Experience Platform ID サービスを実装する必要があります。

   ID サービスは、Experience Cloud コアサービス、ソリューション、People コアサービスの顧客属性およびオーディエンスのための、共通の識別フレームワークですID サービスは、サイト訪問者に一意の永続的な ID を割り当てることで機能します。組織が ID サービスを実装している場合、この ID を使用すれば、異なる Experience Cloud ソリューション内で、同じサイト訪問者と彼らのデータを識別できます。

   ![](assets/mc_id_service_graphic.png)

   ID サービスは、様々なソリューション固有の ID（例えば、Analytics AID）を置き換えることもできます。[顧客 ID と認証状態](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html)機能を使用すると、ID サービスを通じて顧客 ID を Experience Cloud に渡すことが可能になります。ただし、ID サービスは、既に登録されているソリューションのみと連携することに注意してください。他製品へのアクセスにサインアップしていない場合、ID サービスではアクセスが提供されません。

   いずれは、ID サービスは、多くの現在および将来の Experience Cloud 機能、強化、サービスにとって不可欠な要素になります。現在、ID サービスは、[Analytics](https://www.adobe.com/jp/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/jp/marketing-cloud/data-management-platform.html) および [Target](https://www.adobe.com/jp/marketing-cloud/testing-targeting.html) をサポートしています。

   >[!IMPORTANT]
   >
   >Adobe Experience Cloud Device Co-op に参加するには、Experience Cloud ID サービスが必要です。

   ID サービスを実装していない場合、今が移行戦略を検討し始めるチャンスです。ID サービスの重要性と役割について詳しくは、[なぜ新しい Identity Service に注目すべきか](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)を参照してください。

   Experience CloudIDについて詳しくは、「[Experience CloudIDの概要」、「](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html)」、「[Adobe Experience Platform IDサービス](https://experienceleague.adobe.com/docs/id-service/using/home.html)」を参照してください。

1. **Adobe Analytics レポートを有効にします。**

   Analytics でレポートを有効にし、収集しているコンテンツや広告データを確認するには、[メディアレポートの有効化](/help/media-reports/media-reports-enable.md)を参照してください。
