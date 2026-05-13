---
title: プレースメント ID
description: 各広告のプレースメント IDをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 9%

---


# プレースメント ID

>[!BEGINSHADEBOX]

*このページでは、**プレースメント ID**のレポートディメンションについて説明します。 この変数の収集方法については、[配置ID](/help/implementation/variables/ads/placement-id.md)を参照してください。*

>[!ENDSHADEBOX]

**プレースメント ID** ディメンションは、広告プレースメント ID （通常、広告サーバープラットフォームで定義されたスロットまたはゾーン）をレポートします。 ディメンションを使用して、プレースメントスロット間のエンゲージメントと完了率を比較します。

## このディメンションの入力方法

プレースメント IDは、`media.adStart` イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | `a.media.ad.placement`をeVarにマッピングする[処理ルール ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)を作成します。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `evar1`-`evar250`、`post_evar1`-`post_evar250` （処理ルール `a.media.ad.placement`がマッピングされるeVar） |

## ディメンション項目

各アイテムは、`media.adStart`に報告されたリテラル プレースメント値です。
