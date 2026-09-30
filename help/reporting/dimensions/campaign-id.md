---
title: キャンペーン ID
description: 各広告が属するキャンペーンをレポートします。
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
source-wordcount: '122'
ht-degree: 14%
---

# キャンペーン ID

>[!BEGINSHADEBOX]

*このページでは、**キャンペーン ID**&#x200B;のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; キャンペーン ID](/help/implementation/variables/ads/campaign-id.md)を参照してください。*

>[!ENDSHADEBOX]

**キャンペーン ID** ディメンションは、各広告クリエイティブが属する広告キャンペーンをレポートします。 このディメンションを使用して、キャンペーンを共有する複数のクリエイター間でエンゲージメントをロールアップします。

## このディメンションの入力方法

キャンペーン IDは、[広告の開始](/help/implementation/events/ads/ad-start.md)ごとにプレーヤーによって設定されます。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.ad.campaign`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## ディメンション項目

各項目は、[ad start](/help/implementation/events/ads/ad-start.md)に報告されたリテラルキャンペーン値です。
