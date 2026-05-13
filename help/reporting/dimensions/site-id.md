---
title: サイト ID
description: 各広告の広告サイト IDをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 9%

---


# サイト ID

>[!BEGINSHADEBOX]

*このページでは、**サイト ID**のレポートディメンションについて説明します。 この変数の収集方法については、[ サイト ID](/help/implementation/variables/ads/site-id.md)を参照してください。*

>[!ENDSHADEBOX]

**サイト ID** ディメンションは、広告サイト ID （通常は広告サーバープラットフォームのID）をレポートします。 ディメンションを使用して、広告配置サイトごとのエンゲージメントを分割します。

## このディメンションの入力方法

サイト IDは、`media.adStart` イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.ad.site`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.ad.site`がマッピングされるeVar） |

## ディメンション項目

各項目は、`media.adStart`に報告されたリテラルサイト ID値です。
