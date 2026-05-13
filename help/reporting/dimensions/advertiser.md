---
title: 広告主
description: 各広告で取り上げられた企業やブランドを報告します。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 11%

---


# 広告主

>[!BEGINSHADEBOX]

*このページでは、**広告主**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[広告主](/help/implementation/variables/ads/advertiser.md)を参照してください。*

>[!ENDSHADEBOX]

**広告主** ディメンションは、各広告で取り上げられた企業またはブランドをレポートします（例：`"Ford"`または`"Coca-Cola"`）。 ディメンションを使用して、広告主によるエンゲージメントと完了率を分類します。

## このディメンションの入力方法

広告主は、`media.adStart` イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.advertiser`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/ja/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadvertiser, post_videoadvertiser` |

## ディメンション項目

各項目は、`media.adStart`に報告されたリテラル広告主名です。
