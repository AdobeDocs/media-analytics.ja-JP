---
title: ポッド位置での広告
description: 親の広告ブレーク内の各広告のインデックスが0個の位置をレポートします。
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
source-wordcount: '156'
ht-degree: 8%
---

# ポッド位置での広告

>[!BEGINSHADEBOX]

*このページでは、ポッド位置&#x200B;**の**&#x200B;広告のレポートディメンションについて説明します。 この変数の収集方法については、[&#x200B; ポッド位置の広告](/help/implementation/variables/ads/ad-in-pod-position.md)を参照してください。*

>[!ENDSHADEBOX]

ポッド位置&#x200B;**の**&#x200B;広告ディメンションは、親の広告枠の中の各広告のインデックスが0個の位置を報告します。 ポッドの最初の広告は`0`、2番目の広告は`1`などです。 ディメンションを使用して、広告枠の中の位置ごとにエンゲージメントと完了率を比較します。

## このディメンションの入力方法

ポッド位置の広告は、プレーヤーが[広告開始](/help/implementation/events/ads/ad-start.md) イベントごとに設定します。

| レポートシステム | ソース |
| --- | --- |
| Adobe Analytics | [[!UICONTROL &#x200B; メディア広告]](/help/reporting/setup/analytics-reporting.md)が有効になっている場合、コンテキストデータ `a.media.ad.podPosition`から自動的に収集されます。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| データフィード | `videoadinpod`, `post_videoadinpod` |
| Audience Manager | `c_contextdata.a.media.ad.podPosition` |

## ディメンション項目

各項目は整数の位置の値（`0`、`1`、`2`、...）です。 [ad start](/help/implementation/events/ads/ad-start.md)に報告されました。
