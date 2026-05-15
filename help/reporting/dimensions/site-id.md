---
title: サイト ID
description: 各広告の広告サイト IDをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%

---


# サイト ID

>[!BEGINSHADEBOX]

*このページでは、**サイト ID**のレポートディメンションについて説明します。 この変数の収集方法については、[ サイト ID](/help/implementation/variables/ads/site-id.md)を参照してください。*

>[!ENDSHADEBOX]

**サイト ID** ディメンションは、広告サイト ID （通常は広告サーバープラットフォームのID）をレポートします。 ディメンションを使用して、広告配置サイトごとのエンゲージメントを分割します。

## このディメンションの入力方法

サイト IDは、[広告の開始](/help/implementation/events/ads/ad-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.ad.site`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.ad.site`がマッピングされるeVar） |
| Audience Manager | `c_contextdata.a.media.ad.site` |

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告されたリテラルサイト ID値です。
