---
title: サイト ID
description: 各広告の広告サイト IDをレポートします。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
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
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.ad.site`がマッピングされるeVar） |
| Audience Manager | `c_contextdata.a.media.ad.site` |

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告されたリテラルサイト ID値です。
