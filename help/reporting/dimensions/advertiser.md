---
title: 広告主
description: 各広告で取り上げられた企業やブランドを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

---


# 広告主

>[!BEGINSHADEBOX]

*このページでは、**広告主**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[広告主](/help/implementation/variables/ads/advertiser.md)を参照してください。*

>[!ENDSHADEBOX]

**広告主** ディメンションは、各広告で取り上げられた企業またはブランドをレポートします（例：`"Ford"`または`"Coca-Cola"`）。 ディメンションを使用して、広告主によるエンゲージメントと完了率を分類します。

## このディメンションの入力方法

広告主は、[広告開始](/help/implementation/events/ads/ad-start.md) イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.advertiser`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告されたリテラル広告主名です。
