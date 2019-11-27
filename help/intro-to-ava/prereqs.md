---
title: 前提条件
description: null
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 前提条件 {#prerequisites}

## 判断 {#decision}

トラッキングを実装する前に、状況に合った実装方法を見きわめるため、いくつかの点を最初の段階で判断する必要があります。

* **Media Analytics** - 最新のメディア SDK（標準、推奨される実装）やメディアコレクション API（RESTful）を使用
* **マイルストーン** - 以前のアドビのトラッキング実装
* **Data Insertion API** - メディア SDK を使用せずにトラッキングを実装

## タスク {#prereq-tasks}

*Media Analytics* 実装について、開始前に完了しておく必要がある作業を示します。

1. **Experience Cloud を有効にします。**

   Adobe Experience Platform Identity Service を実装する必要があります。

   Identity Service は、Experience Cloud コアサービス、ソリューション、People コアサービスの顧客属性およびオーディエンスのための、共通の識別フレームワークですサイト訪問者に一意の永続的 ID を割り当てることで機能します。組織が ID サービスを実装する場合、この ID を使用することで、同じサイト訪問者およびそのデータを様々な Experience Cloud ソリューションで識別できます。

   ![](assets/mc_id_service_graphic.png)

   また、この ID サービスは、様々なソリューション専用 ID（例：Analytics AID）を置き換えることができます。[顧客 ID と認証状態](https://marketing.adobe.com/resources/help/ja_JP/mcvid/mcvid-authenticated-state.html)の機能を使用して、ID サービスから独自の顧客 ID を Experience Cloud に渡すことができます。ただし、ID サービスは、既に登録されているソリューションのみと連携することに注意してください。他製品へのアクセスにサインアップしていない場合、ID サービスではアクセスが提供されません。

   いずれは、ID サービスは、多くの現在および将来の Experience Cloud 機能、強化、サービスにとって不可欠な要素になります。現在、ID サービスは、[Analytics](https://www.adobe.com/jp/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/jp/marketing-cloud/data-management-platform.html) および [Target](https://www.adobe.com/jp/marketing-cloud/testing-targeting.html) をサポートしています。

   >[!IMPORTANT]
   >
   >Adobe Experience Cloud Device Co-op に参加するには、Experience Cloud ID サービスが必要です。

   ID サービスを実装していない場合、今が移行戦略を検討し始めるチャンスです。ID サービスの重要性と役割について詳しくは、[なぜ新しい Identity Service に注目すべきか](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)を参照してください。

   >[!IMPORTANT]
   >
   >ユーザー ID 情報がメディア専用の呼び出しに存在しない場合、Analytics のデフォルトの[フォールバック ID による方法](https://docs.adobe.com/content/help/ja-JP/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html)が適用されます。

   Experience Cloud ID について詳しくは、[Experience Cloud ID の概要](https://marketing.adobe.com/resources/help/ja_JP/mcvid/mcvid-overview.html)および [Adobe Experience Platform Identity Service](https://marketing.adobe.com/resources/help/ja_JP/mcvid/) を参照してください。

1. **Adobe Analytics レポートを有効にします。**

   Analytics でレポートを有効にし、収集しているコンテンツや広告データを確認するには、[メディアレポートの有効化](/help/media-reports/media-reports-enable.md)を参照してください。

