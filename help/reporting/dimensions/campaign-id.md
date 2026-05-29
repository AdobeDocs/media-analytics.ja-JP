---
title: キャンペーン ID
description: 各広告が属するキャンペーンをレポートします。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 13%

---


# キャンペーン ID

>[!BEGINSHADEBOX]

*このページでは、**キャンペーン ID**のレポートディメンションについて説明します。 この変数の収集方法については、[ キャンペーン ID](/help/implementation/variables/ads/campaign-id.md)を参照してください。*

>[!ENDSHADEBOX]

**キャンペーン ID** ディメンションは、各広告クリエイティブが属する広告キャンペーンをレポートします。 このディメンションを使用して、キャンペーンを共有する複数のクリエイター間でエンゲージメントをロールアップします。

## このディメンションの入力方法

キャンペーン IDは、[広告の開始](/help/implementation/events/ads/ad-start.md)ごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL  メディア広告]](/help/reporting/media-reports-enable.md)が有効になっている場合、コンテキストデータ `a.media.ad.campaign`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告されたリテラルキャンペーン値です。
