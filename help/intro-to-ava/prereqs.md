---
seo-title: 前提条件
title: 前提条件
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 前提条件{#prerequisites}

## Decisions {#decision}

トラッキングを実装する前に、状況に合った実装方法を見きわめるため、いくつかの点を最初の段階で判断する必要があります。

* **Media Analytics** - 最新のメディア SDK（標準、推奨される実装）やメディアコレクション API（RESTful）を使用
* **マイルストーン** - 以前のアドビのトラッキング実装
* **Data Insertion API** - メディア SDK を使用せずにトラッキングを実装

## タスク {#prereq-tasks}

For a Media Analytics implementation, here are the tasks you must complete before you begin:**

1. **Experience Cloud を有効にします。**

   You need to implement the Adobe Experience Platform Identity Service.

   IDサービスを使用すると、Experience cloudコアサービス、ソリューション、Peopleコアサービスの顧客属性およびオーディエンスの共通の識別フレームワークを有効にできます。 サイト訪問者に一意の永続的 ID を割り当てることで機能します。組織が ID サービスを実装する場合、この ID を使用することで、同じサイト訪問者およびそのデータを様々な Experience Cloud ソリューションで識別できます。

   ![](assets/mc_id_service_graphic.png)

   また、この ID サービスは、様々なソリューション専用 ID（例：Analytics AID）を置き換えることができます。[顧客 ID と認証状態](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html)の機能を使用して、ID サービスから独自の顧客 ID を Experience Cloud に渡すことができます。ただし、ID サービスは、既に登録されているソリューションのみと連携することに注意してください。他製品へのアクセスにサインアップしていない場合、ID サービスではアクセスが提供されません。

   いずれは、ID サービスは、多くの現在および将来の Experience Cloud 機能、強化、サービスにとって不可欠な要素になります。Currently, the ID service supports [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) and [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Adobe Experience Cloud Device Co-opに参加するには、Experience Cloud IDサービスが必要です。

   ID サービスを実装していない場合、今が移行戦略を検討し始めるチャンスです。For more information about the importance and role of the ID service, see [Why the Identity Service Should be on Your Radar.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In the absence of any user ID information present on the media-specific calls, the default analytics [Fallback ID Methods](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) will apply.

   For additional information about the Experience Cloud ID, see [Experience Cloud ID Overview,](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) and [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/)

1. **Adobe Analytics レポートを有効にします。**

   To enable reports in Analytics and see the content and ad data you are collecting, see [Media reports enablement.](/help/media-reports/media-reports-enable.md)

