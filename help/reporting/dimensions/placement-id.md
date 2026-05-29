---
title: プレースメント ID
description: 各広告のプレースメント IDをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 10%

---


# プレースメント ID

>[!BEGINSHADEBOX]

*このページでは、**プレースメント ID**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[配置ID](/help/implementation/variables/ads/placement-id.md)を参照してください。*

>[!ENDSHADEBOX]

**プレースメント ID** ディメンションは、広告プレースメント ID （通常、広告サーバープラットフォームで定義されたスロットまたはゾーン）をレポートします。 ディメンションを使用して、プレースメントスロット間のエンゲージメントと完了率を比較します。

## このディメンションの入力方法

プレースメント IDは、[広告の開始](/help/implementation/events/ads/ad-start.md)ごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.ad.placement`をeVarにマッピングする[処理ルール &#x200B;](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.ad.placement`がマッピングされるeVar） |
| Audience Manager | `c_contextdata.a.media.ad.placement` |

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告されたリテラル配置値です。
