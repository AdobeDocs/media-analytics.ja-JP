---
title: キャンペーン ID
description: 各広告が属するキャンペーンをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# キャンペーン ID

>[!BEGINSHADEBOX]

*このページでは、**キャンペーン ID**のレポートディメンションについて説明します。 この変数の収集方法については、[ キャンペーン ID](/help/implementation/variables/ads/campaign-id.md)を参照してください。*

>[!ENDSHADEBOX]

**キャンペーン ID** ディメンションは、各広告クリエイティブが属する広告キャンペーンをレポートします。 このディメンションを使用して、キャンペーンを共有する複数のクリエイター間でエンゲージメントをロールアップします。

## このディメンションの入力方法

キャンペーン IDは、`media.adStart` イベントごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.campaign`から自動的に収集されます。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videocampaign, post_videocampaign` |

## ディメンション項目

各項目は、`media.adStart`に報告されたリテラルキャンペーン値です。
